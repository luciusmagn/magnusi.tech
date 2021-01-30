created = "2019-12-20T17:17:37+01:00"
tags = ["magnusi", "rust", "db"]
title = "[EN/IT] A sled-db wrapper for typed tables"

Some time ago, I started using `Sled` DB in my projects due to its elegant design,
great performance, and other features. I also wanted to finally get into databases
that are NoSQL and allow me to do things myself, such as managing types, tables,
and such.

I went on to create a nice wrapper for `Sled` which gives you a fully typed access
to your own tables and exposes typed iterators.

I have used it to great success on the server-side of the Meedias project, and here is
my implementation:

```rust
#![allow(proc_macro_derive_resolution_fallback)]
#![allow(non_upper_case_globals)]
#![deny(missing_docs, unused_extern_crates)]
#![feature(associated_type_defaults, try_trait)]

#[macro_use]
extern crate lazy_static;

extern crate serde_cbor;
extern crate reqwest;
extern crate juniper;
extern crate rocket;
extern crate chrono;
extern crate serde;
extern crate uuid;
extern crate ring;
extern crate sled;
extern crate old_sled;

use ring::digest::{digest, SHA1_FOR_LEGACY_USE_ONLY as SHA1};

use rocket::request::{FromRequest, Request, Outcome};
use rocket::http::Status;

use serde::{Serialize, Deserialize};
use sled::{Db, Tree};

use std::env;
use std::ops::Drop;
use std::path::Path;
use std::sync::RwLock;
use std::borrow::Borrow;
use std::iter::Iterator;
use std::fs::remove_file;
use std::marker::PhantomData;

#[macro_use]
pub mod macros;

pub mod auth;
pub mod models;
pub mod graphql;

pub use crate::models::*;

lazy_static! {
	/// a global handle to the Sled database
	pub static ref DB: RwLock<Db> = RwLock::new({
		if Path::new("remedias.sled.db.old").exists() {
			let old = old_sled::Db::open("remedias.sled.db.old").expect("failed to open old database");
			let new = sled::open(&env::var("DATABASE_URL").expect("failed to read DATABASE_URL environment variable"))
				.expect("failed to open database");

			let data = old.export();

			new.import(data);
			drop(old);
			remove_file("remedias.sled.db.old").expect("couldn't remove old database");

			new
		} else {
			sled::open(&env::var("DATABASE_URL").expect("failed to read DATABASE_URL environment variable"))
				.expect("failed to open database")
		}
	});
}

/// manages a tree and ensures it's type safety
/// also allows automatic type conversions
pub struct TreeMan<K, V>
where
	for<'a> K: Serialize + Deserialize<'a>,
	for<'b> V: Serialize + Deserialize<'b>,
{
	tree: Tree,
	_k:   PhantomData<K>,
	_v:   PhantomData<V>,
}

impl<K, V> TreeMan<K, V>
where
	for<'a> K: Serialize + Deserialize<'a>,
	for<'b> V: Serialize + Deserialize<'b>,
{
	/// create a new tree manager from a tree
	pub fn from_tree(tree: Tree) -> Self {
		Self { tree, _k: PhantomData, _v: PhantomData }
	}

	/// creates an iterator over (K, V)
	pub fn iter(&self) -> impl Iterator<Item = (K, V)> {
		self.tree.iter().filter_map(|res| {
			if let Ok((k, v)) = res {
				Some((
					serde_cbor::from_slice::<K>(&k).ok()?,
					serde_cbor::from_slice::<V>(&v).ok()?,
				))
			} else {
				None
			}
		})
	}

	/// try to get a value from the database
	pub fn get<Key: Borrow<K>>(&self, k: Key) -> Option<V> {
		self.tree
			.get(serde_cbor::to_vec(k.borrow()).unwrap()) // can't fail
			.ok()
			.flatten()
			.map(|v| serde_cbor::from_slice::<V>(&*v).ok())
			.flatten()
	}

	/// try to insert into database
	pub fn insert<Key: Borrow<K>, Value: Borrow<V>>(
		&mut self,
		k: Key,
		v: Value,
	) -> sled::Result<Option<sled::IVec>> {
		self.tree.insert(
			serde_cbor::to_vec(k.borrow()).unwrap(),
			serde_cbor::to_vec(v.borrow()).unwrap(),
		)
	}

	/// insert a k-v pair
	pub fn insert_pair<Key: Borrow<K>, Value: Borrow<V>>(
		&mut self,
		pair: (Key, Value),
	) -> sled::Result<Option<sled::IVec>> {
		self.insert(pair.0, pair.1)
	}

	/// update a key
	pub fn update<Key, Value, F>(
		&mut self,
		k: Key,
		fun: F,
	) -> sled::Result<Option<sled::IVec>>
	where
		Key: Borrow<K>,
		Value: Borrow<V>,
		F: Fn(Option<V>) -> Option<V>,
	{
		self.tree.update_and_fetch(serde_cbor::to_vec(k.borrow()).unwrap(), |value| {
			let value = value.and_then(|val| serde_cbor::from_slice(val.borrow()).ok());
			let res = fun(value);
			res.and_then(|v| serde_cbor::to_vec(v.borrow()).ok())
		})
	}

	/// update a key
	pub fn update_transform<Key, Value, NewValue, F>(
		&mut self,
		k: Key,
		fun: F,
	) -> sled::Result<Option<sled::IVec>>
	where
		Key: Borrow<K>,
		Value: Borrow<V>,
		NewValue: Serialize,
		F: Fn(Option<V>) -> Option<NewValue>,
	{
		self.tree.update_and_fetch(serde_cbor::to_vec(k.borrow()).unwrap(), |value| {
			let value = value.and_then(|val| serde_cbor::from_slice(val.borrow()).ok());
			let res = fun(value);
			res.and_then(|v| serde_cbor::to_vec(v.borrow()).ok())
		})
	}

	/// remove a value
	pub fn delete<Key: Borrow<K>>(&mut self, k: Key) -> sled::Result<Option<sled::IVec>> {
		self.tree.remove(serde_cbor::to_vec(k.borrow()).unwrap())
	}
}

/// wraps the database
///
/// the reasons are two:
/// 1. to allow  FromRequest implementation
/// 2. declarative table access
pub struct Database<T: Table>(TreeMan<T::Key, T::Value>, PhantomData<T>);

impl<T: Table> Database<T> {
	/// read-only access to tree
	pub fn read(&self) -> &TreeMan<T::Key, T::Value> {
		&self.0
	}

	/// read and write access to tree
	pub fn write(&mut self) -> &mut TreeMan<T::Key, T::Value> {
		&mut self.0
	}

	/// procures a new random u64 key
	pub fn get_key() -> sled::Result<u64> {
		let lock = DB.read().expect("the rwlock has been poisoned");
		lock.generate_id()
	}

	/// opens the databasse
	pub fn open() -> Option<Self> {
		if T::has_get_tree() {
			match T::get_tree() {
				Ok(t) => Some(Database(TreeMan::from_tree(t), PhantomData)),
				Err(_) => None,
			}
		} else {
			match T::get_tree_naive() {
				Ok(t) => Some(Database(TreeMan::from_tree(t), PhantomData)),
				Err(_) => None,
			}
		}
	}
}

/// trait for the Table marker types
pub trait Table {
	/// opening a table might not always work,
	/// this type should explain what's the issue
	type TableError = sled::Error;
	/// type of the key/ID
	type Key: Serialize + for<'a> Deserialize<'a>;
	/// type of the value
	type Value: Serialize + for<'b> Deserialize<'b>;

	/// name (actually prefix) of the table
	fn name() -> &'static str;
	/// gets the actual tree, should do it using the global DB handle
	fn get_tree_naive() -> Result<Tree, sled::Error> {
		let lock = DB.read().expect("the database rwlock has been poisoned");
		// ^ this usually implies a deeper underlying problem,
		// so it's probably okay to hard crash

		lock.open_tree(&Self::name())
	}

	/// should return true if a custom get tree function is available
	fn has_get_tree() -> bool {
		false
	}

	/// optional custom function for fetching a tree,
	/// can call [`Table::get_tree_naive`]
	fn get_tree() -> Result<Tree, Self::TableError> {
		unimplemented!()
	}
}

impl<'a, 'r, T: Table> FromRequest<'a, 'r> for Database<T> {
	type Error = &'static str;

	fn from_request(_: &'a Request<'r>) -> Outcome<Self, Self::Error> {
		if let Some(db) = Database::<T>::open() {
			Outcome::Success(db)
		} else {
			Outcome::Failure((Status::InternalServerError, match T::has_get_tree() {
				true => "failed to run custom db-loading function",
				false => "failed to load database",
			}))
		}
	}
}

impl<T: Table> Drop for Database<T> {
	fn drop(&mut self) {
		let _ = self.0.tree.flush();
	}
}

/// trait for manupulating a newy created entry
pub trait NewEntry {
	/// table
	type Table: Table;
	/// type of the key/ID
	type Key: Serialize + for<'a> Deserialize<'a> =
		<<Self as NewEntry>::Table as Table>::Key;
	/// input type
	type Input = ();

	/// create new
	fn create(src: Self::Input) -> (Self::Key, Self);
}

/// new entry almost finished trait
pub trait NewEntryPartial {
	/// table
	type Table: Table;
	/// val
	type Value: Serialize + for<'a> Deserialize<'a>;

	/// new modify
	fn and_modify<F: Fn(&mut Self::Value)>(self, fun: F) -> Self;
	/// save
	fn save(self) -> sled::Result<Option<sled::IVec>>;
}

impl<T> NewEntryPartial for (T::Key, T)
where
	T: NewEntry
		+ Serialize
		+ for<'a> Deserialize<'a>
		+ Borrow<<<T as NewEntry>::Table as Table>::Value>,
	<T as NewEntry>::Key: Borrow<<<T as NewEntry>::Table as Table>::Key>,
{
	type Table = T::Table;
	type Value = T;

	fn and_modify<F: Fn(&mut Self::Value)>(mut self, fun: F) -> Self {
		fun(&mut self.1);
		self
	}

	fn save(self) -> sled::Result<Option<sled::IVec>> {
		let mut db = Database::<Self::Table>::open().unwrap();

		db.write().insert(self.0, self.1)
	}
}

/// Generuje hash ze zdroje
pub fn make_hash(src: &str) -> String {
	digest(&SHA1, src.as_bytes()).as_ref().iter().fold(String::new(), |mut a, x| {
		a.push_str(&format!("{:x}", x));
		a
	})
}

```

Of course, it will be necessary to delete the cruft to make use of it,
but this should give you a rough idea. Creating tables is then as easy
as this:

```rust
use uuid::Uuid;
use serde::{Serialize, Deserialize};

/// Model instance, tj. 'miniserveru'
/// K instancím se řadí veškerý obsah
/// v projektu Meedias
#[allow(warnings)]
#[derive(Clone, Debug, Deserialize, Serialize)]
pub struct Instance {
	/// Identifikátor instance
	pub id:     Uuid,
	/// Čitelný název stránky
	pub name:   String,
	/// Doména stránky
	pub domain: String,
	/// UUID všech vlastníků dané instance
	pub owners: Vec<Uuid>,
	/// Globální tagy přiřazené dané instanci
	pub tags:   Vec<String>,
}

/// Struktura pro přijímání instance
#[allow(warnings)]
#[derive(Clone, Debug, Deserialize, Serialize)]
pub struct RInstance {
	/// Čitelný název stránky
	pub name:   String,
	/// Doména
	pub domain: String,
	/// Vlastnící (tvůrce je zde automaticky)
	pub owners: Option<Vec<Uuid>>,
	/// Globální tagy
	pub tags:   Vec<String>,
}

use crate::Table;
impl Table for Instance {
	type Key = Uuid;
	type Value = Instance;

	fn name() -> &'static str {
		"instance"
	}
}

use crate::NewEntry;
impl NewEntry for Instance {
	type Input = RInstance;
	type Key = <Self as Table>::Key;
	type Table = Self;

	fn create(src: RInstance) -> (Uuid, Instance) {
		let id = Uuid::new_v4();

		(id, Instance {
			id,
			name: src.name,
			domain: src.domain,
			owners: src.owners.unwrap_or_default(),
			tags: src.tags,
		})
	}
}
```

You can then use the database like this, for example:

```rust
/// fetch instance with domain
pub fn instance_with_domain(domain: String) -> Vec<Instance> {
	let instances = Database::<Instance>::open().unwrap();

	instances
		.read()
		.iter()
		.filter(|(_, x)| x.domain.contains(&domain))
		.map(|(_, x)| x)
		.collect()
}

```

Cheers,
