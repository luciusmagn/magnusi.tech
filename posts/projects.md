tags = ["magnusi"]
title = "Projects"
hidden = true


These are some projects of mine. Of course,
all of them are opensource. Unless specified otherwise,
every project (apart from forks, of course) is licensed
under the [ISC license](https://choosealicense.com/licenses/isc/).
The list is (hopefully) sorted alphabetically.

## alma-hook

A tiny web listener for usage with Github and Gitlab
webhooks. Runs a script on receiving the correct request.
For use on servers.

Repository: <https://github.com/luciusmagn/alma-hook>

## Ambivalence

My environment for editing `troff` documents. When used
with `mupdf`, you can get a live preview that updates
everytime time you save. Uses parts of `plan9port`,
the `wendy` inode watcher, heirloom `troff` and original
Rust code. Includes files provided to me by the venerable
Brian Kernighan himself. He is a really nice guy.

Repository: <https://github.com/luciusmagn/ambivalence>

## async_command

Like the Rust Command type, but with asynchronous
`stdout` piping. Useful for when you want to wrap
a cli program in your code.

Repository: <https://github.com/luciusmagn/async_command>

## boo

A Rust library which extracts the Cow type from
liballoc so it can be used in no-std contexts.
Named `boo` after the sound cows make in my
native language.

Repository: <https://github.com/luciusmagn/boo>

## c2net
A tiny networking library for the C2 programming language.
Made as a proof-of-concept. It is a heavily modified
version of zed_net library ported to C2.

Repository: <https://github.com/c2hub/c2net>

## c2rust-dwm

This is the DWM window manager converted into Rust through
the `c2rust` tool. I am slowly working on cleaning the code
up and turning it into idiomatic Rust.

Repository: <https://github.com/luciusmagn/c2rust-dwm>

## C2TC
C2 Tiny Compiler. Originally intended to be a small
compiler for C2, hopefully free from LLVM dependency.
Very WIP, but it can parse 100% of C2.

Repository: <https://github.com/luciusmagn/c2tc>

## c2vector
A tiny vector library for the C2 programming language. Nothing
more to be said.

Repository: <https://github.com/c2hub/c2vector>

## deck

Deck is a presentation program created by `fdehau`. I added
a dark theme and remote presenter support into my fork.

Repository: <https://github.com/luciusmagn/deck>

## Gjkbot
A simple bot for Github, which moves repositories
and checks for repositories, which have been
'handed in'. Ran as a cronjob on my Raspberry Pi in
conjuction with the update script from the Snapshot
repository.

Repository: <https://github.com/rust-gjk/gjkbot>

## gjk.cat [CZ]

The [gjk.cat](https://gjk.cat) platform servers for managing study materials
in a sane and frugal way. Generates static mdBook webs
with a hierarchy of teachers, subjects, categories and
materials.

Repository: <https://github.com/gjk-cat/gjk.cat>

## hyper-rat

A tiny static site generator that matches up templates
with contexts and contains no extra features except for
Markdown support. Surprisingly flexible. Only has 165 lines
of code and 7 top-level dependencies.

Repository: <https://github.com/luciusmagn/hyper-rat>

## ipc-rs

A Rust library that maps the System V IPC API. Currently
only supports message queues. Using message queues is a
nice way to do inter-process communications, since you
dont care if one of the processes crashes. The messages
will still be stored in the given queue. Used to be used
in `remedias`. Beware that real-world usage might require
tweaking kernel parameters.

Repository: <https://github.com/luciusmagn/ipc-rs>

## light_pencil
My fork of Sharp Pencil, which is a fork of Pencil. Pencil
is a Rust web microframework inspired by Flask. For my
intents, Pencil was too big and taking too long to compile.
My fork contains many simplifications, unfinished and broken
stuff removed, clippy lints fixed, updated dependencies,
unneeded stuff removed and stripped from everything else
I didn't need, including documentation. The codebase has
been roughly halved, dep count lowered by five and compile
times pleasantly decreased.

Repository: <https://github.com/luciusmagn/light_pencil>

Update: I made an even smaller fork called `pen`, Link
here: <https://github.com/luciusmagn/pen>

## mags_game

This is a `raylib-rs` game I am currently developping.
The goal is to create an extremely branching and bizarre
text adventure where even most mundane of choices will
lead to completely different outcomes.

Repository: <https://github.com/luciusmagn/mags_game>

## Markov
Implementation of Markov chains. Based on orangeduck's
program from his artistic coding blog. Daniel's
implementation is in Python, my is in Rust lang.

Repository: <https://github.com/luciusmagn/Markov>

## micro-config
One file C# library for making tiny config files. Not
much else to be said. Doesn't support many types.

Repository: <https://github.com/luciusmagn/micro-config>

## microtest
A few lines in a C header to test your C code. Can print a
pretty verdict if needed. Really handy if you don't have
resources or need for a real testing framework. Based on
ideas presented in an article I read a few years ago.

Repository: <https://github.com/luciusmagn/microtest>

## MiniLinuxFS
Small generator of an absurdly small statically linked
Linux filesystem. The default configuration contains
most common UNIX tools and Bash but only has about 4mb.
Thanks to being statically linked and not containing
any complicated programs, it is very secure.
Used for testing students' script in Learnshell at
the ČVUT college.

Repository: <https://github.com/luciusmagn/minilinuxfs>

## morpho

A more featureful static site generator which I created
from `mdblog` for use with this website. See the post
about SSGs to learn more about it.

Repository: <https://github.com/luciusmagn/morpho>

## net_47sb_59vm
A small http server written in C#. It contains a
support for modules written in any .NET language
thanks to dynamic assembly loading.

Repository: <https://github.com/luciusmagn/net_47sb_59vm>

## Pebble & Pebble-server
Package manager for C2 language libraries. Packages for Pebble are
called pebbles. Mimicks Cargo in many ways. Has
really nice coloring. Uses Clap, which is a great
command-line argument library.

## recipe-reader
A Rust library for reading (and writing) C2's recipe files, which
are needed for compilation. Pretty efficient, but has unconventional
API which needs a refreshment.

Repository: <https://github.com/c2hub/recipe-reader>

## Rhai & Nary
A small, embeddable and fast interpreted programming language
written in Rust. It is pretty early into development,
but already shows some promising qualities. Originally
written by Jonathan D. Turner. I am a maintainer and Developer
since fall 2017.
Nary is my experimental fork with a lot of dangerous
code and multithreading.

Rhai repository: <https://github.com/jonathandturner/rhai>  
Nary repository: <https://github.com/luciusmagn/nary_lang>

## rsremote

A Rust program which uses SSH and `rsync` to remotely
compile, test, check or benchmark Rust code. This is a
fork of `cargo-remote` which added several new features,
most notably the ability to remotely compile an entire
Cargo workspace. Since these features were later implemented
into `cargo-remote` itself (I thought it was a dead project,
so I did not create a pull-request), `rsremote` is mostly
obsolete.

Repository: <https://github.com/luciusmagn/rsremote>

## Rustgrade
A client/server for managing students' grades. It is just
a small example of how to use UDP for networking and TOML
Serialization/Deserialization with Serde.

Repository: <https://github.com/rust-gjk/rustgrade>

## rusting

A joke library for Rust error handling.

Repository: <https://github.com/luciusmagn/rusting>

## Rustkr
Some of the excersizes and programs from K&R implemented
in C, but embedded in a Rust catalogueing program. The
purpose was to learn about FFI in Rust in a way that
isn't as painful as translating C2TC is/was.

Repository: <https://github.com/luciusmagn/rustkr>

## Rusty
A tiny build-system for C/C++/ASM. Written in C and
uses the mpc library for parsing its configuration
files called rustyfiles. It has nothing to do with Rust
language. Rusty was written long before I knew Rust
existed. The name meant 'A program to refresh my Rusty
C programming skills'.

Repository: <https://github.com/luciusmagn/rusty>

## rx

A pixel art editor written from scratch by `cloudhead`. It
has been my editor of choice ever since I discovered it. I
contributed a few features, hence why I am listing it here.

Repository: <https://github.com/cloudhead/rx>

## sic

This is the `sic` suckless IRC client. I have modified it
to have a cleaner message syntax and added highlighting.

Repository: <https://github.com/luciusmagn/sic>

## simple_io

A Rust library for simple access to IO. For use
in programming competition to speed up coding.

Repository: <https://github.com/luciusmagn/simple_io>

## Stackbomb
A collection of programs testing how deep can you go in
nested calls till you blow up the stack. Please contribute
more languages if you want to. Haskell is surprisingly
good.

Repository: <https://github.com/luciusmagn/stackbomb>

## tinybeard

A modification of the greybeard Sublime Text 3 theme to
be much smaller, removes unnecessary gaps and uses a
smaller custom font (ProFontExtended).

Repository: <https://github.com/luciusmagn/tinybeard>

## TSGui
Graphical interface for TShock Terraria servers. Very pretty,
but people from elevators keep breaking it. I don't really
play Terraria anymore.

Repository: <https://github.com/luciusmagn/TSGui>

## Wren.NET

A simple .NET wrapper for the Wren programming language.
As far as I am aware, this was the first .NET wrapper in
existence, however, it has been superseded by others and
it is not up to date with the latest versions of Wren.


Repository: <https://github.com/luciusmagn/Wren.NET>
