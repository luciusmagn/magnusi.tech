tags = [""]
hidden = true

<style>
	html {
		background-color: #fff;
		filter: invert(1) hue-rotate(180deg);
		min-height: 100vh;
	}
	body {
		font-family: "Fanwood", serif;
		font-size: 1.4rem !important;
		min-height: 100vh;
	}
	main {
		margin: 0 auto !important;
	}
	.post p {
		text-align: justify;
		text-justify: auto;
	}
	blockquote p {
		color: #646464;
	}
	p em {
		font-style: italic;
		font-family: "Fanwood Italic", serif;
	}
	img {
		filter: invert(1);
	}
</style>

A B C D E F G H I J K L<br>
M N O P Q R S T U V W X<br>
Y Z 0 1 2 3 4 5 6 7 8 9

a b c d e f g h i j k l<br>
m n o p q r s t u v w x<br>
y z . , ; : ? ! > < ( )<br>
{ } < > @ # & ° \ / " '<br>
| ^ [ ] § \* \_ - + \` ~

# oifoidsoi

- stygian
- serendipity
- halcyon
- agastopia
- perpendicular
- accolade
- omen
- augur
- bona fide
- epiphany
- bravado
- afficionado
- nada
- brogue
- cacophony
- gibbous
- caustic
- encumber
- colloquial
- asunder
- smithereens
- kindred
- macabre
- sojourn
- elysian
- genteel
- transpire
- raillery
- auspicious
- sophistry
- transmogrify
- nimiety
- obviate
- methinks
- assay
- naught, aught
- dregs
- drought
- shrewd
- mayhaps
- vale
- wont
- hereby
- thus
- yonder
- harken
- corse
- amicable
- lackaday
- eerie
- prithee
- sepulture
- nary
- inadvertently
- whence
- alow
- betwixt
- anon
- yede

# wqážtcdwýžt

```c
module c2stack;

import stdlib local;
import stdio local;
import string local;

//Implementation of a stack in C2
public type stack struct
{
    void** items;
    int32 capacity;
    int32 total;
}

public func void init(stack* s)
{
    s.capacity = 4;
    s.total = 0;
    s.items = malloc(sizeof(void *) * s.capacity);
}

public func int32 total(stack* s)
{
    return s.total;
}

func void resize(stack* s, int32 capacity)
{
    void** items = realloc(s.items, sizeof(void *) * capacity);
    if (items != nil)
    {
        s.items = items;
        s.capacity = capacity;
    }
}

public func void push(stack* s, void* item)
{
    if (s.capacity == s.total)
        resize(s, s.capacity * 2);
    s.items[s.total++] = item;
    printf("%d %s\n", s.total, item); // only debug
}

public func void* pop(stack* s)
{
    int32 index = total(s) - 1;
    if (index >= 0 && index < s.total)
    {

        void* src = s.items[index];
        void* dest = malloc(sizeof(src));
        memcpy(&dest, &src, sizeof(src));
        delete(s, index);
        return dest;
    }
    return nil;
}

func void delete(stack* s, int32 index)
{
    if (index < 0 || index >= s.total)
        return;

    s.items[index] = nil;

    for (int32 i = index; i < s.total - 1; i++)
    {
        s.items[i] = s.items[i + 1];
        s.items[i + 1] = nil;
    }

    s.total--;

    if (s.total > 0 && s.total == s.capacity / 4)
        resize(s, s.capacity / 2);
}

public func void free(stack *s)
{
    stdlib.free(s.items);
}
```

# msdmopas bananananana
basic custom ranking script for terraria (JIST)

```js
var k = 10;
var rankupbitch = acmd_alias_create("buy", 0, 0, "ranks.up", function (player, args) {
            var num;
            alert(num);
            var groupname = player.Group.Name;
            alert(groupname);
            if (groupname == "default" || groupname.indexOf("player") != -1) {
                if (groupname == "default") {
                    num = 0;
                    alert(num);
                } else if (groupname.length == 7) {
                    num = parseInt(groupname.substring(groupname.length - 1, groupname.length));
                    alert(num);
                } else {
                    num = parseInt(groupname.substring(groupname.length - 2, groupname.length));
                    alert(num);
                }
                var cost = (num + 1) * (num + 1) * 1948;
                alert(cost);
                var secAcc = seconomy_get_account(player);
                alert(secAcc);
                seconomy_pay_async(secAcc, seconomy_world_account(), seconomy_parse_money(cost), "a new rank", function (payResult) {
                    if (payResult.TransferSucceeded == true) {
                        tshock_exec(tshock_server(), '/user group "' + player.Name + '" player' + String(num + 1));
                    } else {
                        tshock_msg(player, "Sorry, you don't have enough money. The next rank costs " + String(cost) + ".");
                    }
                });

            } else {
                tshock_msg(player, "You are not a part of this ranking system. Contact staff if you think that is an issue.");
            }
});
```

# pokdaspokdsakpo
```js
//Data library for /shop command. In the place where item is written, type any random name. Please avoid duplicates. You can make some system in the naming though

/******************************************************
 * Info:
 *  itemDataQWERTY - name of the data holder. Because JIST code is shared with all the C sharp code and other JIST codes, it has to be unique to avoid conflicts. Thats why QWERTY
 *  "item" - inner id of the item property of the data holder, itemDataBitches. Every "item" has to have unique name.  See below what I mean.
 *  "XitemPrice" - Representation of SEconomy price
 *  "Xcmd" - what is to be written as the first parameter of /shop. Identifies the item. It is custom. Please avoid stuff with spaces.
 *  "Xitems" - array of items to be added to players inventory. If a name of an item it contains more than one word, encase in '\" \"' instead of plain " ". 
 *  "XmaxQuantity" - Self-explanatory, maximum number of items player is able to buy at once. Just so it is avoided to have 20 Tera Blades stuffed in one slot.
 *  "Xhidden" - if set to true, it will not show up when doing /shop list.
 *  "XpricePerMax" - if set to true, then the XitemPrice is price for the maxQuantity, not. Otherwise, it is price for one piece. If the quantity parameter is not used a true XpricePerMax will try to buy whole XmaxQuantity, while false XpricePerMax will buy just one at once.
 *
 * Command Arguments:
 *  /shop (name) [quantity] - buys an item. If using quantity, the price is dynamic. If you buy a 40 dirt and the dirt will have XpricePerMax set to true and the XmaxQuantity set to 64, the user will pay 40/64 of the price.
 *  /shop test - requires special permission. Prints out all info about all items to the console. For debugging.
 *  /shop see (name) - views price, name and max quantity. Requires special permission
 *  /shop help - prints this. Regular users won't see /shop ON/OFF and /shop test.
 *  /shop ON/OFF - disables/enables the shop. Enabled by default. I suggest you disable the shop in time you meddle with SEconomy
 *
 * Permissions:
 *  shop - enables buying, /shop list, basic /shop see and /shop help for a player
 *  shop.shutdown - enables /shop ON/OFF
 *  shop.see - allows player to see all information about an item with /shop see, not just price, max quantity and name.
 *
 * Instuctions:
 *      Put shopConfig.js and shopScript.js to serverscripts folder. This script requires SEconomy, JIST and cmdAliases installed in order to run.
 *  Add items by copying the "item" : {} block as below. Paste before last : null and change the "item" to something else. 
 *  The "item" thingy is an unique identifier. If you have two of the same name, the second will overwrite the first and so on.
 *  Check out the examples if you don't understand the gibberish I speak. Don't forget to remove the examples before using the script.
 *  Don't forget the comma after each property. Every little mistake can break it, just like every other config, JSON, etc. In case of problems,
 *  message me on either steam ( display name = magnusi, steam name = luciusmagn ) or skype ( display name = BANÁÁN :3, skype name = luciusmagn )
 ******************************************************/

/********* TEMPLATE *************
"item": {
            "XitemPrice": 0,
            "Xcmd": "sponge",
            "Xitems" : [],
            "Xhidden": false,
            "XpricePerMax": false,
        },
***********************************/
var itemDataQWERTY = {

    //ACESSORIES
    "accessories": {
        "item": {
            "XitemPrice": 0,
            "Xcmd": "sponge",
            "Xitems" : [],
            "Xhidden": false,
        },
        "anotheritem": {
            "XitemPrice": 0,
            "Xcmd": "banana",
            "Xitems" : [],
            "Xhidden": false,
        },
        "last": "null"
    },



    //ARMOR
    "armor": {
        "item": {
            "XitemPrice": 0,
            "Xcmd": "sponge",
            "Xitems" : [],
            "Xhidden": false,
        },
        "anotheritem": {
            "XitemPrice": 0,
            "Xcmd": "banana",
            "Xitems" : [],
            "Xhidden": false,
        },
        "last": "null"
    },


    //VANITY
    "vanity": {
        "item": {
            "XitemPrice": 0,
            "Xcmd": "sponge",
            "Xitems" : [],
            "Xhidden": false,
        },
        "anotheritem": {
            "XitemPrice": 0,
            "Xcmd": "banana",
            "Xitems" : [],
            "Xhidden": false,
        },
        "last": "null"
    },
    "last": "null"
};
```

# sšěeě
big boss death

[Scene shifts back to the graveyard. Snake is in a sweat.]


**???**              : That's right. Good. No need for you to go just yet. It's
                   been a long time... Snake.

**Snake**            : Big Boss?

**Big Boss**         : Let it go... My son. I'm not here to fight. Or should I call
                   you brother?

**Snake**            : What?

**Big Boss**         : It's over. Time for you to put aside the gun... And live. It
                   all began with a bunch of old fools. Now... They've all
                   passed away. Their era of folly is over. I'm the only one
                   left, and soon... I'll be gone, too.

**Snake**            : How can you still be alive?

**Big Boss**         : That body Liquid burned on the Volta... Wasn't mine. That
                   was the body... Of a clone. Solidus.

**Big Boss**         : He was a perfect clone. Zero, and the proxy AIs that came
                   after him, were convinced that Solidus was me. I was
                   implanted with nanomachines... Kept in a state of eternal
                   sleep... By JD the proxy AI. They had me sealed away
                   completely... Not only physical body, but my will, too. The
                   technology was similar to what they used to restrain the B&B
                   members you encountered. For me to wake again... The System
                   had to be destroyed... One way or another. Ocelot and EVA
                   wanted two things... To bring me back to life, and to end
                   the Patriots. That meant destroying the AI and killing the
                   man... JD and Zero. Right before you uploaded the virus into
                   GW... The way to JD was opened, but only through the
                   physical manifestation of GW. That's when we finally learned
                   the location of this man... Zero. For me, and for them...
                   For Naomi... Nothing was more important. And it was for that
                   they put their grand scheme into motion. EVA stole my body
                   from them and reconstructed it by replacing the missing
                   parts with pieces from Liquid and Solidus. And Ocelot... In
                   order to fool the System... Used nanomachines and
                   psychotherapy to transplant Liquid's personality onto his
                   own. He used hypnotic suggestion to turn himself into
                   Liquid's mental doppelganger. For all our advances in
                   nanotechnology... Information and genetic control... They've
                   never managed to control people at will... Let alone turn
                   one person totally into another.


**Big Boss**         : Under certain conditions, someone can be made to play a
                   specific role... Act like someone else. Cats... Do love to
                   play as snakes. It all started with him... Zero.

**Big Boss**         : Zero grew old, and by the end, his Patriots were being run
                   by a network without shape or form.

**Snake**            : What do you mean without shape or form?

**Big Boss**         : The proxies were only one small part of the vast cycle that
                   Zero created. The corporations, for-profits... And research
                   institutions that comprise the military-industrial complex
                   were part of it, too. They operated on budgets automatically
                   allotted to them by the proxies... Accounts maintained by
                   the Patriots. The network covered everything from weapons
                   R&D and investment to production and marketing. It
                   encompassed the people, the companies - even the laws that
                   protect them. Politics and economics became nothing more
                   than iterations of the same oppressively uniform system. I
                   don't think anyone realized that it was all a setup... A
                   mere set of norms. The Patriots were those norms - a neural
                   network reduced to its simplest form. That's what they
                   really represented... Uniformity without individual will,
                   without change. But then one day, those norms suddenly
                   deviated from that pattern, and underwent a mutation. It was
                   like the birth of a new life form... The System found a new
                   way to propagate itself... War. The norms the Patriots had
                   crafted for their unified state quickly became dependent on
                   a single business... The war economy. Meanwhile, the
                   political cause of creating a "cleaner, safer battlefield"
                   provided a convenient catalyst. By then, the System was no
                   longer being steered by Zero's will -- or anyone else's. It
                   was then that the norms - manifested as AIs, the inheritors
                   of Zero's will... Began to reproduce and take on a life of
                   their own. Zero's original intent was to carry on The Boss's
                   will and establish a unified world state... An inside world.
                   But his successors failed to carry on his will. Eventually,
                   JD became the very age itself, propagating its will as it
                   pleased. And this age chose to act through economics instead
                   of nation-states. Powered by the industrial and digital
                   revolutions that came before it... this age gave birth to a
                   twisted economic revolution - a battlefield revolution. It
                   created a new world without substance. In this new world,
                   there were no ideologies, no principles, no ideals... Not
                   even the thing she treasured most... Loyalty. There was only
                   the war economy. It was a colossal error in judgment - one
                   Zero couldn't possibly have foreseen.

**Big Boss**         : With the American system in a state of collapse... The
                   Patriots' society has reverted to a blank slate. This man
                   was the source of it all. And he doesn't even realize it.
                   He's completely unaware of the fact that he led the world to
                   the brink of ruin. Even with so much bad blood between us...
                   It's funny... Now that I'm actually face to face with him
                   again... The hatred is gone. All I feel is a deep sense of
                   longing. And pity. Did Zero really hate me? Or... Did he
                   fear me? It's too late to ask him now. The original
                   members... Para-Medic... Sigint... EVA... Ocelot. They've
                   all passed on. Only Zero is left. Everything has its
                   beginning... But doesn't start at "one." It starts long
                   before that... In chaos. The world is born... From zero. The
                   moment zero becomes one is the moment the world springs to
                   life. One becomes two... Two becomes 10... 10 becomes 100.
                   Taking it all back to one solves nothing. So long as zero
                   remains... One... Will eventually grow to 100 again. And
                   so... Our goal... Was to erase Zero. Even the mighty
                   Patriots began with a single man. That one man's desires
                   grew huge... Bloated. Absorbed technology began to
                   manipulate the economy. We realized too late... That we had
                   created a beast. We had helped turn Zero... Into 100. His
                   sin... Was ours. And for that reason... I'm taking it upon
                   myself to send Zero... Back to nothing.

**Snake**            : You going back to zero, as well?

**Big Boss**         : You erased me two times before. Today... Will mark the third.
                   The FOXDIE Zero planted in you... It's already begun eating
                   away at my body. Truth is... The FOXDIE in you... Is what
                   killed EVA... And Ocelot.

**Snake**            : What are you talking about?

**Big Boss**         : Naomi... She told me... Everything.

**Snake**            : What's wrong?

**Big Boss**         : They did it again. They used you to kill me. The Patriots.
                   No... Their proxies... In order to bury us... They did it
                   again. In the end, they're no more than a program. All they
                   can do is repeat the same pattern over and over again. Do me
                   a favor, will you? Take me over to her. There's one more
                   thing Naomi wanted me to tell you. About the... Old FOXDIE
                   in your body... The only that mutated. The new FOXDIE inside
                   you continues to multiply. At the same time... It is
                   preventing the old... Mutated FOXDIE from reproducing. The
                   new FOXDIE is uprooting the old. Naomi confirmed it in her
                   follow-up. The mutants are receding. Before long, they'll be
                   gone entirely.

**Snake**            : Does that mean the mutant strain won't cause an epidemic?

**Big Boss**         : It will only live as long as you do. But event then... The
                   process will just repeat itself. One day, the new FOXDIE,
                   too, will start to mutate... And become a new threat. But
                   that is, if you manage to live that long.

**Snake**            : Am I going to die?

**Big Boss**         : Everyone dies. You can't stop it. You can't run away from
                   it. Let me tell you something... Don't... Don't waste the
                   life you have left fighting. I've never thought of you... As
                   a son. But I've always respected you as a soldier. And... As
                   a man. If you'd been in my place back then... Maybe you
                   wouldn't have made the same mistakes that I did. Ever since
                   the day I killed The Boss... With my own hands... I... Was
                   already dead. Boss... You were right. It's not about
                   changing the world. It's about doing our best to leave the
                   world... The way it is. It's about respecting the will of
                   others... And believing in your own. Isn't that... What you
                   fought for? At last... I understand the meaning behind what
                   you did. At last... I understand the truth behind your
                   courage. It's almost time for me to go. And with me... The
                   last ember of this fruitless war dies out. And at last those
                   old evils will be gone. Once the source of evil returns to
                   zero... A new one... A new future... Will be born. That new
                   world... Is yours to live in. Not as a snake... But... As a
                   man. Know this... Zero and I... Liquid and Solidus... We all
                   fought a long, bloody war for our liberty. We fought to free
                   ourselves from nations... And systems... And norms, and
                   ages. But no matter how hard we tried, the only liberty we
                   found... Was on the inside... Trapped within those limits.
                   The Boss and I may have chosen different paths... But in the
                   end, we were both trapped inside the same cage... Liberty.
                   But you... You have been given freedom. Freedom to be...
                   Outside. You are nobody's tool now... No one's toy. You are
                   no longer a prisoner of fate. You are no longer a seed of
                   war. It's time for you to see the outside world with your
                   own eyes. Your body... And your soul... Are your own. Forget
                   about us. Live... For yourself. And find... A new lease on
                   life. Boss... You only need one snake. No... The world would
                   be better off without snakes. This is good... Isn't it?

[Big Boss's cigar falls out of his mouth as he grows weak]

[Big Boss takes his final breath as the scene ends.]

# dsaeewwqq

My first operation will be soon. I am not scared about the operation
or the pain, but what is next. It is not good to be away from my classmates
for two months. I feel like for two months my life stops but their goes on
without me.

# ewqewqewq

I was thinking about what is important. Now, I am convinced that the
two most important things are loyalty and honesty. All other values can be
made from them. Love is ultimate honesty and ultimate loyalty. Bravery
is being loyal to your ideas when in danger or fear. Friendliness is both
loyalty and honesty. Endurance is a form of loyalty to yourself. And wise is
to be honest to yourself and the world. You can also define patience,
willpower, integrity, confidence and a lot of more with honesty and loyalty.
It is also reciprocal, loyalty is honesty to your values and relationships,
honesty is loyalty to yourself and others.

# kowddddd

It is some time since my operations. I cannot walk for a long time yet,
but I learned to jump on one leg very good and to be fast with crutches.
They are a multi-tool. But it is lonely, I am separated and my classmates
and my three girl friends seem to be losing interest. I understand,
I am just so far away. Most of the day, I am lying in bed. Sometimes,
grandma is here with me and talks to me and helps me with things. I will
pay her back in the future. Being like this is not practical. But when
I am here like this alone, my brain starts to work and think about things.
The world is weird and complex, but thinking about it and people brings me
some joy, if I figure something out.

# mkewklwelk

My recovery went differently than I thought. I filled the hole of people
with reading and studying. I love new information. I read and saw videos
from very man fields, I didn't care about what it was, just if I didn't know
it before. It is strange, some things in world work how I did not expect them
and what I believe is challenged always. That is good, isn't it?

# cmcmcmcm

I am back at school, but things have changed. The boys who don't like
me were "working" on my reputation when I was gone. I am now at the
edge of the class and I was thrown out from my seat. The girls are
still nice to me, but I am only like accessory now. It hurts. The blonde
one is the nicest to me. I am not sure why. Maybe she is more loyal?
Not sure.

# ijoiojo

There were two courses. England and skiing. I was a bit excluded,
but they were nice otherwise. The girls didn't care much about me. I think the Russian
guy had completely undermined me. He is now popular with the ladies and he
does not like me. He was jealous I talked to girls first. I also won a bet
to get one girl's number. It was because he was stupid, acting like a dumb and not normal
around girls.
It was bad one day in England when most of the class went for pizza. There were
many people, my three girl friends too, but the boys decided that only me can't join
or even tag along so I do not get lost. My girl friends did not helped me, they
just pretended I don't exist and let the boys push me out of the pizzeria. I was walking
alone after that for some time.
Another day, we were on the beach and the boys started throwing stones on me
and my feet. Already it was hard with my operated foot to walk on the beach,
the thrown stones hurt.
But I spoke with some new people too. There is this dark-haired one girl. I did not
know she was in the class too last year. She likes anime and cool things too. We
did together a lot of fun things on the ski course.
At ski course, my girl friends sat at a four people table. I was with them the
first day, but then another girl took my place without asking. I was mad at first,
since I had to sit at the "outcast table" but then I realized she needs them as friends
more than I do.
But I got along with the girl I mentioned before. She was at the outcast table too.
Otherwise, the skiing course was just big leg pain and I had inflamed toes, but I do not mind.

# dsdsds

The winter was pretty. Snowy trees. Silence just snow cracking. Peace. Long nights.
Smoking homes. Playing with snow. No mosquitoes. Hard to get up in the morning. Christmas.
But being alone. Warm home. Gaming with two classmates from elementary school. One
of them is a bit dangerous.

# hjvfnd

It will be holidays soon. I am offline and more away from people. There is no internet
so it's hard to talk to them. I like it there, but it is very lonely. I try to fill my
time with other things. A lot of offline programming, downloaded books. Studying random
things.

# daklsdlksakdsalkcmsc

I forgot to mention one thing before the holidays. I do gardening. I have a tiny secluded
garden under one apple tree. I have a lot of tiny plants there. I like my tiny plants,
they make me happy. It is my tiny kingdom. I am doing chemical experiments on the flowers,
I am trying to figure out what makes a good fertilizer. It looks like some plants can grow
in sawdust. Funny, haha.

# vosdpvovkxlycm

My second operation is coming up. Now I know what to expect. The boys still don't like
me and the girl friends are acting even weirder this year. The result will be the same.
I think. I will need one or two more surgery. This one should be less bad, I shouldn't
bleed as much and be disabled for as long as the first one.
I have been playing a lot of Terraria multiplayer lately, it is nice. I am on a good
server.

# ewqqqqqqqqqqqqqqqqqqqqqqqqqqqqqq

The operation was much better than the first. Not as painful and now I knew what to do.
Again I am learning, my grandma is visiting me and I count days until my return to school.
When I was in hospital I had just my tablet. I played Osmos on it. It is a fun little game.
There was a guy next to me, he was half-Bulgarian. He was only year older than me but he
had a beard like a 30 year old. I think he was a bit autistic, he was obsessed with cars,
both toy ones and real cars. I added him on Steam and on Skype. His usernames are BMW models.
What the hell. Cool guy otherwise.

# pofewpokfewpo

My time in Terraria is great. It improves my English tremendously. I am meeting a lot of
people there and I developed an idiosyncrasy that everyone can identify me with. It is
saying 'howdy'. I like 'howdy'. It's just me saying that. Haha.
However, there some less fun things. I got a special position in the community now,
I am a moderator/admin and I am considered the universal conflict defuser and people
come to talk to me when they feel troubled. No one knows I am just 14, everyone thinks I am
20+. But it is so strange and sad to hear how many people have issues in their life.
Some of the things are kinda dark, self-harming, depression, suicide attempts, delusions,
feelings control, trauma. I wonder why it is.
I try to help everyone to calm down and stabilize and get them to seek help.
Sometimes, they come back with good news. Other times it is sad.

# Laurensbananananbagr

I have a good friend in Terraria and online in general for some time already.
He is called Laurens and he is like a brother to me. One of my best friends not just
online but overall. He does programming and computers as well and he has a good sense
of humor. Sometimes he likes to do damage for fun (we hacked some competitors' servers,
and drew penises over the maps hehe). We play games together and we talk about all
sorts of stuff. He is the son of a Belgian billionaire (or just extremely rich guy) and
he lives in a palace (Laurens has his PC room on the other side of his dad's car collection)
but one could never tell. His parents raised him right.
We talk about his relationship and our friends too. Laurens has a girlfriend, she is
his high-school classmate and originally comes from Poland. He likes her very much.
Other than that, Laurens has troubles remembering names, so he makes nicknames.
For example, the blonde girl friend is "Ms. Boobs" there is also "minecraft girl",
"the tall one", "snarky bitch", "the bear", "the Russian" and "the one who has hair
like a girl". He refers to my friends from elementary as communist party members
because of the cringy roleplay me and them do.

# der programmierererer

Recently, I got to know a dutch guy who is creating a programming language.
I wanted to make my own version, so I wrote him an email if he would mind and
if he would give me some direction. The email was very dumb and I think it sounded
condescending. But the guy was very nice. Eventually, it turned out that my idea
does not make sense, so I joined the development of the real version. It is very
fun and interesting to develop a programming language. A lot of planning and
theory goes into it and it is fun to see that you can create things
with the thing you made. I think that programming is art too.

# gggggggg

My recovery is almost over. I kinda flunked school. I spent most of the time
studying random fields that interested me instead of doing school work. This
will be tough, heh. Both my math and physics professors are already promising
me tests as soon as I return. Oops. At least I learned some new things.
Thanks to the experience with the people in Terraria, I am more interested
in how humans work both physically and mentally now.

# dssaadadddd

It is some time since I returned to school. I am now even more on the outskirts.
One of my former girl friend now hates me very much and I don't know why. She kicks
and punches me and she tripped me on my crutches as well. At one time, she stepped
on my operated foot just to scare me away from the girls. I have become a thing
of the past for them, just a nuisance. It hurts very much, I miss them everyday.
Strange.

# eddede betrayal

I went through the conversations I had with Ms Boobs as Laurens calls her. I conclude
that she is a very manipulative and two-faced person. Her niceness is just pretending
so she can profit from people. In every conversations in the last few months, she
makes excuses, telling me that she will tell things later or speak to me later, but
never fulfills her promises. She only messages me when she needs something, but
she doesn't say so at the start, she first does small talk and pretends interest
and only like an hour later comes out her real goal. I do not think I will call her out
on it, I will just act dead and dumb until I am left alone.
Shame, this evil witch enchanted me, and even although I know how rotten she is,
I still feel something towards her. It sucks. I will have to wait this out.

# sdsads

Another summer holidays are upon me. Isolation and relaxation, being offline for two months.
Looking forward to gardening,
I bought some strange tiny plant a few days ago. I don't even know what is it called,
but it is cute. Also, it looked like my tree is going to die despite the entire family's trying,
but it survived. It still looks quite sick, but it will survive.

# truth

I have done a lot of thinking during the summer. I am now certain that one should
always tell the truth or at least not lie. I think it can be defined as such.
One of thinking about yourself is that you are just one grain of sand among seven
billion. And when you think about yourself like that, you might think that "what
difference does it make what I say or do?". This might happen to be a very convenient
mode of thinking for you because if it doesn't matter what you say or do, then you
don't have any responsibility and you can do whatever you want. This comes as a bit
of nihilism (it's the price for it I mean), but if you can just ignore any
responsibility like that, then a small bit of nihilism is a small price.
This appears to be the underground motivation for nihilism.

But there is another more accurate way to look at this.
You can imagine that you are single node in a network (like a single computer on the internet),
and you can do some calculations very fast to figure out how powerful you are in that network.
A person can know about a thousand people, probably more as they get older.
These thousand people also know a thousand people. That means that you, as a person
are one person away from a million people (that is there is just one person between you
and a million others) and two people away from a billion.

And you are the center of this network of a million billion people. And information
within a network propagates in a network manner. In programming, we would call this
peer-to-peer connections, this model.

So do not underestimate the power of what you say and do. We as western society
have figured it out a long time ago - through the concept of logos, from the Bible
and earlier, the Greek culture. This means that the capacity for speech is divine,
it is what creates order from chaos, it is what sometimes turns bad order into chaos.
This means that one should not underestimate the power of truth. Nothing is more
powerful.

Now, in order for someone to speak the truth, they have to let go of the outcome.
It means "Alright, I am going to say what I think. As stupid as I am, biased as I
am, ignorant as I am, I am going to state what I think as clearly as I can,
and I am going to live with the consequences no matter what they are."

This is part faith, the idea is that nothing brings a better world into being than
the stated truth. That might cost a price, but that is fine, you are going to pay
a price for every fucking thing you do, and every fucking thing you don't do. One
doesn't really get to choose not to pay a price, but only which price they are going
to pay.

Then if you are going to stand up for something, stand up for your truth. It shapes
a human being because people will respond to your truth. They will respond, object,
tell you why you suck, why you are a biased moron and why you are ignorant, and
if you listen to them, then you will be just that much less like that next time
you say something. And doing this only for a short time improves a person's life
tremendously (also according to the psychiatrists). A person becomes much more
tough and articulate and able to communicate and withstand pressure. One might
not recognize themselves. They will become a force. I have been practicing this online
and it feels like the right way forward. And one should start doing that now, not
holding it off. Stop lying, start telling just the truth.

But people might be afraid, they might feel that it is not safe to speak. This seems
to be more commonplace now. To address that - it is not safe to speak and it never
will be, but the thing you need to keep in mind that it is even less safe not to speak.
It is a balance of risks. It is like you want to pay the price for being who you are
and stating your mode of being in the world or do you want to pay the price a shitty
slave? A serf? Someone who is enslaving themselves? That is a major price. It takes
time to unfold and you will just wind up a miserable worm at the end of that: no
self-respect, no power, no ability to voice your opinions, nothing left but resentment
because everyone's against you because of course you never stood up for yourself.

So, say what you think, carefully pay attention to your words -> it is a price you want to
pay if you are willing to believe that truth is the foundation of society and in the
most real sense, if you are willing to take that leap, then tell the truth and see
what happens. Nothing better could possibly happen to you, there will be ups and downs
of course, there might be push-back and controversy, but it doesn't matter, the truth
is what makes the world not hell.

So tell the truth or at least don't lie. Truth may bring short term conflict, especially
at the beginning, but it brings long term peace and stability, and learning. With each
day I have adopted this view, my horizons broaden and my eyes are opening to new things
about myself and others.

Some of the people I talk to online can't talk, or they are afraid to talk,
perhaps they are in such as a state that they feel like they have nothing to say, and those
are real problems, but if you can, start talking and sharpen yourself. Stand your ground,
don't apologize for what you haven't done and especially for what you haven't been accused of
(like wtf dude, why would you make show weakness/insecurity by doing that? don't apologize for
things which beget no apology).

# hackerbroo

Lately, I have been getting acquainted with the Rust programming language. It's pretty
cool. Currently, I am mostly doing C and C#, but Rust might be the next big thing. It still
isn't 1.0, so they are changing things a lot, but I like the core concepts. Rust
focuses on the functional paradigm, security, speed and concurrency and the performance
it achieves is just superb. I heard that there will be like a final IT class project,
I think I am going to make something in Rust just to get a feel of the language. It
also interfaces nicely with C language.

# íéeripo

Last days, I made a new interesting friend. He is one of the troubled people too,
but he is very smart. Conversations with him are eye-opening, he has an interesting
perspective of things. Kinda different to Laurens, he brings new information to the table.
He had a very tragic life story, it completely explains his struggles, bad family,
misfortune, brain cancer, personality issues due to the cancers, failed suicide attempt,
depressions, anxiety, but things are starting to turn for the better for him.
He will do good on himself in no time.
Also there is no one as good as him in PVP. He wins 1v5s with a fucking touchpad.
Can you imagine that? A fucking touchpad!

# ifvdsdvs

I have become a counsel to many online. It seems that people like me and seek me out.
This is cool. I don't do much, I just listen, I am patient and I don't get affected by
their problems. So many people nowadays have no one who will listen to their issues
and not get fed up with them...

# aaaaaa

I got lost in the forest a while ago. It is such a beautiful serene place. I found my
way towards a lake. It used to be a popular place for swimming many decades ago, but it
has been abandoned and now genius loci rules over this place. The atmosphere there was really
quite something. I have never seen grass I would like more than the one by this lake.
I tried to build a shelter there to chill and reflect. Hopefully, it will last until summer holidays.

# daspads333333

Another surgery is upon me. This one will be more difficult than the other two. They will
be doing to my right foot in one operation what they did to the left in two. It seems that
this will also be my longest recovery yet. However, if all goes well, it will be my last surgery
for some time. Maybe there will be another one to remove all the metal from my feet, but the
doctor isn't sure yet. Funny thing to mention, it turns out that my feet, my constant source
of pain, are so specific that the doctor took pictures of them for students. He had me stand
on a special mirror-y stool and do poses so that my special feet can be documented as an interesting
medical case to teach about, haha. What a fun way to be special.
As for the recovery, I expect the usual. At this point, I have been forced into the role of
outcast within the class. I don't mind that much anymore. I just wish I was included in
some social activities, it gets lonely sometimes. But, a tiny handful of friends to depend on.

# dsadwqdew

This one hurt quite a bit. I reckon that it will take a very long time until I can walk again
as I used to. For the most part, I have been lonely and my classmates, with very occasional
exceptions, do not seem to care about me. I do not mind that much. I am trying to meet the solitude
with learning and try to become stronger for the future. Also, it lets me think in peace.

# qewqeqweq

My recovery is underway just as it was planned. Once again, I spend most of my time playing Terraria,
Borderlands and studying a variety of fields, not just IT. Recently, I have taken a particular
interest in psychology, sociology and biology. What I am trying to find out and figure out for myself
are the connections between these three. I am a firm believer that most psychological and sociological
findings are rooted in biology, or rooted in something that itself is rooted in biology.
To put it differently, Nature sets the playing field and gives a basic set of norms. These are mostly
unshakable. What we do within this environment is up to us, those are the psychological and cultural
findings.

# aasdads

I have a Terraria server now, we are actually the 4-5th biggest server in the world. Me and Laurens
are running it with two other friends, Jewsus and Slayer. Jewsus is a strange Australian basement
dweller, he just plays games and smokes weed most of the day, but he is not a bad person and he has
a lot of experience running communities. He is pushing 30, after all. Slayer is a twenty-something
American pedo. We call him a pedo as a shitty nickname because he was once flirting with a girl
on the server, not knowing she was fifteen. However, not to worry, he isn't actually a pedophile
and there hasn't been a single incident or a complaint or any attempt to flirt with anyone. Boy
just make a rookie mistake of not asking for age first, haha. His nickname, Slayer, actually
has a funny backstory. It goes: "One day, I was at home completely hammered after coming home
from a night out with the boys and I wanted to play some MMORPG, but I couldn't make up a new
nickname, my brain just didn't work. So I looked around the room until I spotted a Slayer album,
and then I was like, aha! Slayer it is."
Slayer is paying the server costs and everything, pretty cool guy. And no one except Laurens
knows I am a teenager, haha.

# cdscdsc

On the new server, I can talk with even more people. This in combination with my experiences
led me to conclude that I have not been fully realizing the impact family can have on a person.
I am grateful for the family I have, for if they have not been as good as they are, I feel
like I could have easily fallen prey to some very dark times and toxic stuff. Many of the people
I talked don't have such vigilant and good at upbringing parents. Some have or had parents
which were counterproductive to their children's healthy development.
Perhaps, I will be a parent once too. I feel that should do everything I possibly can
to be the best father I can possibly be. To be there, to teach what is important, to care for
and to defend my family, to notice the early signs of bad things happening to my children.
I vow to do so and to never break this promise.

# qreee

It has been some time since I returned to class. This one was a harder return, I have lost
a lot of strength and I didn't have the physical power to stay for all lesson at first. I still
have crutches and I hope to put one away soon, and the other after a month and a bit or so.
Except for my very few friends, I am no pretty much secluded from the rest of the glass. Those
who dislike me continue to undermine me, but they can no longer do anything to hurt my spirits,
most others have learned to live without me.
However, this puts me in an interesting position. I can be a good outside observer. I am enjoying
this so far, I am starting to see more patterns in human behavior, I am able to uncover hidden
connections and I can, with some success, predict what is going to happen between people with
a relative success. I am playing the predicting game nearly constantly and I am getting better
at it. I think it will come in handy someday.
This is related to another game I have, it is (de-)aging faces. When I was small, it was
unfathomable how could someone very young get old and have a similar face to very old people.
I felt like there are actually three human species, young/children, adult and old. Obviously,
I knew that isn't true even then, so I tried to figure out the missing links. I can now pretty
accurately tell how old  people looked young and how young people will look in old age. Babies
are still an enigma.

# jfjhjfghjfhj

Lately, I find myself having stronger and stronger urges to express myself artistically,
to express what lies inside, my visions, dreams, ideas and experiences. I am a very visual
person, I like to arrange things in a visually pleasing manner. However, I have very little
ability and I find it hard to be proud of what I make. Most of the attempts to write or draw
end up discarded and I am very reluctant to show to someone the things I kept.
My mind is that of a storyteller, constantly producing stories and plots and projecting
them to me in daydreams and at night in real dreams. I find daydreaming to be an interesting
phenomenon, I will have to do an analysis later.

# qwpoewqe

I am becoming disillusioned with the stance of people who seem to have used to be like-minded.
For as long as I remember, I have been left-leaning on the political spectrum and I represented
what I consider to be sensible left values. Lately, something has started happening within
the western left wing. Winds of radicalization have started blowing and I can spot budding seeds
of Marxist rhetoric appearing within my communities. I also find that the common left-wing
representative is losing the ability to debate properly, instead seeking to use arguments
ad hominem, strawman arguments, argumentative fallacies and ignorance towards facts. It is
scary, I think that it will do no one good and that it will lead to a great societal divide
between people who need not be divided. Connections are important, people, value them. We
need to stay connected.

# daskosa

It seems to me like many people are not cautious enough when it comes to meeting new people.
A not so long ago, there was a saying about not getting into cars with strangers and about
trust and verification, but it seems many are forgetting them now. I fear that this unwillingness
to ensure your own safety can be the undoing of many people. It is perhaps also a side-effect
of a surge of hedonistic lifestyle and of the fallacious ideology of "living in the moment",
which is ultimately a self-destructive shortsighted outlook on life. I think I will get back
to it later, this begets a deeper analysis.

# íšíšíšíší

Memory, recollection. I tried comparing with some people and online and trying to piece together
the extent to which memory serves others and it seems that I have an exceptionally good memory.
The only one I could find who bested me is, as Laurens calls him, The Bear. I have pretty much
a complete recollection since 2-3 years of age, I remember a lot of useless details and also
useful information (and also probably about a 100k memes haha - not that I would remember them really
actively, but I can recognize pretty much any meme I have seen before).
This does not only have positive sides. For one, it turns that people are cyclical in nature
and they tend to repeat themselves. They will repeat with you certain conversations after a certain
period. My advantage is that I remember the conversation from the last time, so I know what
to say to make it a pleasant conversation. If the person is someone I like, I usually tell them
they have told me this before. This could also be used to lie to person and tell them exactly
what they want to hear, but I feel like that would be breaching my moral code and the importance
of truth I have outlined before. Having this memory also means that I do not forget not only what
good things have people done to me, but also how they have wronged me. People, and this is
a psychological fact, usually have a reset duration of about two to three weeks, if you fuck
up, waiting for this long will usually be enough for the incident to leave their active
consciousness and allow you to fix shit up. This does not work on me and neither on The Bear,
so if someone wrongs us, we have no other option than to either forgive or hold a grudge. In
essence however, learning to forgive might not be a bad idea in the long run.

# eden:((

My tiny garden was destroyed, the plants wiped out and the apple tree above it felled,
my little piece of not-so-Outer Heaven is gone. It was my great aunt and great uncle, they
told me that the plants "grew back into the ground by themselves". Plants don't do that for
fuck's sake. There was a tiny maple tree in my garden. Not only can it not grow into ground,
it is also a relatively invasive species, very hard to get rid off naturally. Ah... shame,
I liked it, it's been a lot of good work.

# oěkewpf

Lately, I have been having a repetitive dream and daydream. It always starts with me as magnusi
falling from a great height and crashing into the sea. I break through the surface and I end up
sinking all the way to the bottom. It is not a very deep see. I can always see the surface.
And I just keep staring up at the waves and watching them. It is soothing.

# asdkkmdkkdkdkdkkdkdkdkdkdkd

Even today, with a long of period for hindsight, I still think that loyalty and honesty
are the best virtues one should focus on. That and the ability to pay attention to things.
And combine that with telling the truth. I find that adhering to these values makes things
better and straying from them causes problems. It is therefore important for one to develop
these as far as they possibly can to ensure their individual existence doesn't lead to
ruin.

# adspklcndsclk

It appears my worry about Marxists appearing within left wing and trying to manipulate
it for their own ends and secretly conning trusting people into their agendas was
not unfounded. There is one thing I find particularly heinous - they abuse mentally ill
people and people who aren't doing well. They lull them with a sweet promise of belonging
and good intentions, they tell promise them changing them the world and appeal to their
empathy. And this works because generally, left wing ideas, even radically left wing ideas,
sound good on paper, unlike right-wings, which might seem counter-intuitive at first,
especially to young idealistic people, but may turn out to be actually more developed
than the leftist alternative. There is another problem which allows this. One difference
between left wing and right wing is their attitudes towards borders and categories, in
all meanings of the words. Left wing dislikes to make order in things, categorize them
and create borders, whereas right wing does the opposite. This leads us to the issue
of when does a political ideology go to far. With right wing, especially to the drawing
borders policy, it is pretty easy to define. For right wing, it is the identity politics
devolving into claims of racial and ethnic superiority and moral justification based on
these claims. But for left wing avoids categorization, it does not want to be split
and sorted into a okay/too-far division. Most people would probably tell you they
don't know. Tough luck. And yet, left can definitely go too far. I am not sure about
this yet, but I believe that it is when they start advocating equity (equality of outcome,
aka the reason Marxism produces so many corpses), diversity predicated on ethnic identity
politics and inclusivity. Equity is the greatest demon of these. I wonder how long
it will take for the mainstream to recognize these issues, but for now, I think it will only
get worse. I might go into this deeper, I think that the [diversity, inclusivity, equity]
array requires more explanation, since all of these sound good on paper.

# adspdpoas

Yesterday, I had a long discussion with one of the Terraria people I know about suicide.
By discussion, I mean talking him out of it. It took quite a long time and a lot of
mental strain. And yet, I don't feel emotionally shaken or deeply impacted, I wonder
why it is. The only feeling I felt was compassion, perhaps it was like an instinct or
something, but all the dark stuff the guy had to say came to me as just facts to work
with and debate. Luckily, I succeeded and he promised he would seek professional help.
So I am hoping things will turn around. I wonder how would the content or the outcome
differ if I were impacted.

# sadcodcspoc

Lately, I have taken a keen interest in eye contact. It seems that eyes are a very
important medium of communicating. A good exercise in a room full of people is figuring
out who makes eye contact with whom and when. Human eyes are hypersensitive to eyes
and the direction their pointing. Imagine being in a classroom, you can tell if a person
from the other side of the room is making eye contact with you or looking at your chin.
The angular difference? Extremely tiny. This is a really important evolutionary trait
for humans as pack animals. If I can't see where you are looking, I can't trust you,
and I can't communicate with you. This is why it is scary in horror films when a
character has full black eyes. As for the eye contact itself, it communicates both
relationships and power dynamics. People tend to make eye contact with people they
like the most. Also the ones they dislike, but that is a more hateful eye contact,
you can tell. For the people they are indifferent about, it will probably be little
to no eye contact unless the person becomes the speaker in the group.
For power dynamic, the person who makes consistently longer eye contact than the
person they are making eye contact with has the greater power in the conversation.
In essence if you want to dominate someone, or at least even out the playing field.
People also make longer eye contacts with people they are attracted to, but to differentiate
this, one needs to take into account other characteristics. Sometimes, perhaps when
the people are angry, they try to ignore someone they wouldn't usually ignore.
This is funny to watch because they still accidentally make eye contacts,
then they are like "oops, I am trying to ignore this one" and quickly shift away.

# dsapkkcpodsvds

So turns out that the need to organize ourselves in a social hierarchy is primarily
biological and inherited. According to research, this need is as old as lobsters.
Lobsters have it too and organize themselves similarly. Human antidepressants work
on lobster and help low status individuals become high-status. The most interesting
thing about all this is that lobsters are older than the trees. There is something
older in you than trees that dictates some basic principles of how we organize ourselves
in that world. There is a counter in your brain that takes social status and has
a profound effect on both your psychology and by extension biology: every health
issue is much worse if you are low status, even if you take out things like resources
and access to medical care, and if you are low status, you are also much more sensitive
to negative stimuli, which sometimes leads to manifestation of certain mentally illnesses.

# uzrtefdsdf

In the last few months, I have been talking to a lot of people online, this includes
both "online" people and IRL friends. I have been starting to notice some patterns in
the language we use. It seems that the depth and quality of the interpersonal relationship
depends to a degree on ability to establish common tongue. I call these "microlanguages",
although something like a "microdialect" might be a better term, I am not sure. In
essence, when you are talking with a person for some time, you start to using language
in a specific way, adopting idiosyncrasies that are personal to the parties involved
in the chat, usually two people. It seems that the more members a conversation has, the
lower chance it becomes so tight that everyone would be such good friends with everyone it.
These idiosyncrasies involve language, grammar, vocabulary, linguistic oddities the people
invent, but also usage of emojis. The same people tend to use emojis in a slightly different
way when talking to different people. Provided there isn't anything hampering the language,
like a language barrier, a speech or impediment or a "puritan" approach to language,
then the establishment of a successful interpersonal relationships depends to a degree
on being able to establish a common tongue, create common idiosyncrasies and to adopt
idiosyncrasies of each other. This is in essence a small localized form of cultural
appropriation (which is not always wrong, don't listen to the ideologues uninformed
yelling, they are not social scientists, I might write about this later). And when
you establish such a language, you differentiate yourselves from the general populace
in the way you talk with each other. Sometimes this common tongue can be starkly
different to the norm and perhaps also uncomfortable for the norm, this is particularly
evident for the younger folk (also I think that when exchanging linguistic idiosyncrasies,
you have a greater tolerance upwards, that is, you can better stand the language of those
who are a few years older than those who are a few years younger). In essence, this allows
you to create a small tribe right here in the 21st century. Riveting!
Two more things. A certain non-mainstream social platform has rolled out in full effect
"reactions", this allows you to tag messages of others (sometimes even yours, but
that rarely ever has any utility) with emojis, to signify your general attitude
towards the message and respond without saying anything. I consider it partially
detrimental because people, instead of exercising their typing ability and providing
meaning in a conversation, might steer to just tag your message with an emoji "and go
fuck yourself". However, I believe that the manner in which people use reactions,
as in which emojis for which purpose, will become a part of microlanguages too. One
thing that I would like to research are Snapchats, to see how the picture aspect
correlates with the text. Unfortunately, I think that Snapchat, just like most
mainstream social media, sucks dick and is detrimental to human relationships.
The other aspect I wanted to mention is what I call "defense markers", these are
specific words or phrases which are included by the two parties into the microlanguage
as a means to defending from outside invasion. Usually, these are offensive, vulgar
or so specific words and phrases (or they are used wrong on purpose), that they
are incomprehensible. These then ward off possible outside influence/incursions
and increase the level of connection between the microlinguistic tribe. In essence,
we say offensive and vulgar things without the offensive or vulgar meaning attached to
it, through this we create a barrier from people who are very not like-minded and
ensure that only someone who is very like us can join in on the conversation. A
defense technique, yes.

# epofwkfoewfpo

I want to go back to the cultural appropriation issue before I forget. It is
unusual for me to write two entries into this journal so close together.
Let me put it this way. This is, of course backed up and expressed by years
and years of social and psychological research, not something I would just
invent myself out of the blue to be provocative and what not.

So, for me to understand you, I have to imitate you. That is the ground of understanding.
It is not like I listen to what you say, think about it and then react, although
we do that too, to some degree. It is that I watch you, I look at what you are
looking at, I listen to the flow and rhythm of your voice, I adjust my body
so that it is in accordance with yours, if we are having a real conversation,
I have to. We have to create a space between us that's a consequence of a mutual
imitation, even changing the way that we speak (probably related to my microlanguage
research, haha) because I am going to adjust the way I speak to the way you speak
and the other way around or we are not going to have a conversation. We have to
enter into the same space (a cliche, yes), but all of that is a consequence of
deep and often unconscious and implicit imitation, and to say that cultural
appropriation is a mistake is to deny people the ability to deeply imagine
each other. Because there are conversations going on that a man should never
write a woman's role in a book, movie or a play, or a white person should never
write a black person's role. It is like: All you are doing is forbidding
the creator to project him or herself into the landscape of that other person and
try to truly not just empathize, but go way deeper than empathy,
to try to live out their experience to the best of their imaginative ability in
a deep way and maybe one that can be communicated with other people. You know,
like, maybe a white guy who writes about black experience, and he is careful about it,
can bridge a gap that no other person can bridge, and even though it might not be
a hundred percent accurate, and, not to say that biography itself or autobiography
is ever a hundred percent accurate, it's the best we can do with regards to climbing
inside someone else's head and attempting to truly walk a mile in their shoes.

Undeniably, this does not cover malevolent caricature of other culture's characteristics,
one which is meant to be hateful - not to be confused with playful/offensive humor,
where you make fun of stereotypes, often to precisely show how bizarre the stereotypes are,
but retards will tell you are propagating these stereotypes anyway and that you are the bad
guy for even including a mention of these, like what the hell - but ones that are meant
to be hateful and advocate for racial superiority or actively attempt to discredit
some groups culture as a whole, that is bad. But that is not cultural appropriation.
Calling that cultural appropriation is a misappropriated term.

Do not fall into the radically ideological trap of this hidden claim that it is bad
to learn from and imitate other people. That is stupid. This ability to imitate one another
has been, according to not only biological evidence, one of the things that allowed
us to survive for so long. When one monkey goes, does something stupid and gets a really
bad result which begets a certain solution, the other monkeys don't have to go through the
same ordeal. They can imitate the solutions and the things the first monkey did without
the danger. Through imitation, they can share information about what to do and push
the chaos back a little and reduce the collective suffering in life. Do not be angry
at cultural appropriation just because an idiot on Tumblr or a corrupt intellectual hack
decided that they are smarter than decades if not centuries of biological/evolutionary,
psychological and philosophical research.

# opwmcwdpowww

I have been having another magnusi dream lately. There is a temple far in outer spaces
it is a temple, looking like something the Aztecs built, but grayish and darker. It
is somewhere in outer space on a chunk of torn out land with small vegetation. It is
enveloped in a sphere of dark gray smoke, possibly a part of a barrier which establish
breathable atmosphere and temperature inside the sphere. I go there every time and I
am struck with melancholy and weakness. I sit on the stairs for a minute, then go
inside. Inside the temple, there is a heart.

# wfeijoijfwewioe

Laurens, my friend of a few years by now, had a break up a few days ago. His polish girlfriend
left him and sadly, he is devastated. Turns out she was in it for the money in a big
part and after a few years, she figured out Laurens's dad is not a piggy bank and actually
tries to have Laurens and his identical twin Vincent live normal lives and value money
appropriately. Laurens truly loved her, it's a shame, he is very down right now. At least
she was honest about stating what her goal was and not inventing some story about Laurens
being a terrible person. I will have to watch out for the motivations of not only women
I might like, but people in general, in my future life. Laurens is once again proving to
be my view several years into the future. I think I will go play some games with him
to cheer him up. Recently, I came across a goofy zombie game and he seems to like those.
Or we can play Far Cry or Borderlands.

# asdijviosdfds

Some time ago, I had a strange experience. It was around Christmas, I was going with
the 9 tram for a big chunk of its stations when I see a gypsy woman trying to snatch some
woman's purse. Now, the woman was quite short and skinny, but she deflected the gypsy
woman pretty well, didn't even need the help of her friend, who was a much more taller
and robust girl. Now, I was in a particularly talkative and commentating mood, so I
joking uttered a mildly offensive remark about "gypsies not even being able to steal right",
and to my surprise, the girl heard me and burst out laughing. She and her friend then went
over to me and started jokingly listing out places where she knows gypsies lurk at night
and trying to enlist my knowledge as the "local" who definitely knows where not to go at
night. After some joking about that, the conversation swerved to who I am and who she is,
where she comes from, etc. etc. I tried to speak in plural and get the dark-haired girl
involved too, but she was the closest thing to an ice block in that moment.
When I was about to get off (they were going all the way to Zličín and curiously not by
metro), I asked her for her name, so we can keep in touch and she was "Yea, great idea"
and told me. Interestingly, the name was so specific that I had no worry someone else
would have the same name, probably not in the entire world.
We got along and she invited me for a talk and a walk while she was at work and we
struck a pretty good conversation. She was very smart, but also down to earth and
practical in many things, coming from a small village. Although traffic lights were a bit
of a strange concept for her and I had to warn her not to walk into the oncoming traffic
on a few occasions. In further meetings, there was also the fun aspect of neither
of us paying attention to the world, while we were talking, so in public transport,
we would end up in random places all around Prague.
Another funny fact to mention is that before we added each other on Facebook, we
apparently thought the other was much older. I thought she would be like around twenty
and she thought the same about me (yes, I do like kinda older than I am sometimes),
but turns out neither of us is an adult yet. She is one year older than me though.
I make up for it by being by a head taller even when she had platforms on.
There is a connection, but unfortunately, I don't think anything will be out of it.
Her situation kinda sucks. Her father had abandoned her and her sister when she was
very small (the birth of this girl was actually a totally smart idea of her parents
to mend their dissolving relationship by having another child), her mother is disabled
and very hard of hearing (phone calls are kinda comical, even though I feel bad about
it, because Sára has to yell her lungs out if her mom forgets her hearing aid),
their monetary situation is not great, she has a pretty shit ex-boyfriend, who
by way of being a small village, she bumps into all the time and he isn't very
mature about it, even though he is several years older, and she has to work tremendous
hours to pay for her intr (? not sure about the term) and to cover her food and studying
costs. Not to mention her school being highly demanding in terms of homework.
So unfortunately, I don't think there will be anything of it, despite there being
a connection. There is simply no time.

# acmpvcmspovpodvdspomvodspmvdsv

Turns out there are patterns everywhere, and that humans are fundamentally pattern-seeking
animals. We have known this for years. The reason for this is twofold. In nature, humans
are both prey and predators, which is a rather unique position, and both of these required
us to seek patterns.
The predator part is the easier, we are seeking out patterns of the animals that are hiding
from us, so that we can hunt them. We notice the patterns in their behavior and their way
of life, so we can figure out when and where to strike so we have a successful hunt. And
we needed a successful hunt to survive the winter.
For the prey part, it is similar but it has more implications. We seek out the patterns
on the bodies of predators. There exists a built-in biological fear of snakes in humans.
The working theory right now is that there existed a species of large snakes which preyed
on humans. There is some evidence to suggest that, but it is not yet certain, according to
what I read. And so humans have to learned to notice the snakes, to see their pattern
in the green. Eventually we got better and better at this probably because the humans
who were not good at noticing snakes and other predators were much more likely to get
eaten by one. Then one day 'bam', we learned to see the snake in the future and voila,
humans now have true consciousness. And this allowed us to think about the future
unlike animals, who work on instincts and don't really think about past, present or
future. This revealed to us two things. First, that we need to work. And working means
bringing the hardship and suffering of the future into the present to make it manageable.
You work on your home and food for winter, sacrifice time and go through hardship doing that,
since most work is not what you want to do, but in return, you don't die in the winter
freezing and hungry. In a larger and current day society, the principle is fundamentally
the same, but it is not immediately visible due to the monumentality of it and separation
of interests (people doing just one job), but if everyone stopped working, the result would
be the same, people dying in the winter.
The second thing is that we need to delay gratification. Sure it would be nice, to
eat all the plants we picked up right now, but if we plant half of them, we will have some
security in the future and it will pay off, we will have more to eat later, the gratification
will be all the more. This is why you cannot simply 'live in the moment'. If you do,
you will eventually nosedive into the ground pretty hard. Some may not survive this
crisis. So you need to think in the long term, you need to think in consequences,
you need to pay attention to the future, and you need to make plans! You can't just
live in the moment and hope things will sort themselves out. Because if you don't seize
it, things gravitate towards entropy and sure, they will sort themselves out without your
intervention, but most likely in a way that makes you deeply resentful and miserable.
So think, watch for patterns and use your ability to consider the future.

# asdpadopadoksadpokasdpoad

Lately, I have been pondering about the true meaning of loneliness, and I have come to
think that it does not come from having to people around you. For many years now,
I felt to be alone, and in a way, I am still alone because, at risk of sounding egotistical,
I know, study and hint at things which my peers apparently know nothing of, and to a great degree,
do not want to know or notice. As it turns out, loneliness does not come from having to people
around you or no one to talk to you, but from being unable to share and communicate things
and ideas that seem important to you, or from holding views which others find unacceptable
without considering them for one minute. This is perhaps the true reason I keep
this journal alive, to let out in an orderly manner what I cannot share with anyone else.

# asdpkvdposkvpovdpovdk

Haha, this works, funny.

```
fn main() {
	break rust;
}
```

and it nets you a snarky compiler error about trying to break Rust and whether you want
to have some ICE with that.

ICE stands for Internal Compiler Error.

# dasokdpadopkasd

Love at first sight. Being completely enamored the first time you talk to someone. The foolishness
of the impulsive "i go as my heart goes right now" lover. I have been thinking about these, especially since
I see misery from this happening within the people I know, Laurens too, but I will talk about him later.
So what is the problem? People can be unbearably blind and irresponsible when it comes to relationship
without stopping to think for a minute for longterm implications and objective view on what they are doing.

Let me talk about the problem, and explain how it works according to the psychology research. These
are facts, not opinions.

So you go out with a new person. What do you do? You project a fantasy on them,
and then you fall in love with the fantasy. And you can say "aren't you stupid"
because you're gonna find out that the match between your fantasy and the actual
person is wonky at best. Carl Jung would call that a projection of the anima/the animus,
the anima is the feminine aspect of man that he projects onto the woman in this scenario
he finds desirable like this, animus is the male aspect of woman that she projects onto the man in this scenario
she finds desirable. It goes both ways. And you think: "Oh, he/she is the perfect man/woman",
and the question is: "How do you know that? You have barely gotten to know that person for
a few seconds." But it takes a hold of you and it is an action of instinct. You fall in love
with the image.

Interestingly enough, what you do in a relationship that works is that you actually see,
and what you actually project on the other person, is what could be. Things could be that,
but it is going to take you a hell of a lot of work because you got no shortage of flaws,
and the person has no shortage of flaws either. So you are bringing your flaws together and
that's going to produce a lot of friction and you are going to have to in a lot of dialogue
before you approach that level of perfection again, but maybe you can do it. Then you
maybe get to live with the person. That sounds nice.

And this is a principle in the ways meaning forms in human beings. The unconscious meets the
unknown and it meets it with imagination and fantasy and dreams and art, that is how it is.
So you do not just go from what you do not know to fully articulated knowledge in one step,
that is impossible. One has to extend "tentacles" of fantasy and imagination into the unknown,
that is what theorizing is like, even scientifically. You don't know something scientifically,
you generate a theory, well it is an imaginative representation that your unconscious is helping
you generate and so you meet the unknown with fantasy, that is why we have fantasy, from the
psychoanalytic perspective. That is what dreams do, fundamentally.

You can see why you dream about the future. What is the future going to be like? Well, one
probably has a little imaginative story going on and you do not really create it, you mostly
just watch it unfold, maybe you can tweak it to a degree, but it sort of comes to you from the
wherever the hell things like that come from. From the unconscious, that is the psychoanalytic answer,
it is not really much of an answer, since that is more like a representation of a place
that we do not understand, but that is where creativity comes from and some people are really
creative, all the way down to the core.

And so we often see people who are high in the trait openness (which is pretty much equivalent to intelligence,
as it turns out according to somewhat new research), and these people go everywhere and they
are not always very orderly. And these people are often funny and smart, and they may have the most
nihilistic intelligence one can imagine, just self-critical and brutal to themselves, and these just
criticize themselves out of existence. If you want to help them, you need to tell them to stop listening
to their chattering self-critical rationality and go out and create something, put their massive
creativity into use. Instead of destroying themselves with feelings of insufficiency, just go out
and make something. As long as they are doing that, they are engaged in the world and happy as hell,
creating brings them great relaxation, but as soon as the self-critical rationality comes in
and shuts down the creativity, they get pretty miserable. And this discovery leads me to believe
that I myself should start being less critical about my artistic side.

It is because if someone is really open, then they are a tree with many trunks and if they
are creative and they are not engaging in a creative enterprise, then they are just like
a very sick tree. This is not a trivial realization, this is deeply rooted in human biology.
Creative people need to be creative in order to survive.

But wow, I sure as hell did diverge from what I wanted to say originally. Let me return
back to the topic of relationships. So here is what you should do to have a good relationship.

Watch your person carefully, and whenever they do something you would like them to do
more of, tell them that that was really good, and mean it. And this is not manipulative,
because it is not a lie and because if it were manipulative, it wouldn't work. It is like
you have to say "hey, I am so glad you did that", you have to be precise, "here is what
you just did that I thought was great" and you may get a reaction of the other person being
happy that you noticed. And you know, you do that a bunch of times, and the other person
will be like a rat that's just pushing the lever from cocaine (if you know B. F. Skinner's
experiments). And B.F. Skinner noticed it a very long time ago, that reward is extremely useful
in terms of modifying behavior, but the problem is that it is very hard to notice when things
are going right, because from nature, humans are far more sensitive to when things go wrong.
So people use threat and punishment more often as agents of shifting the people
you're around because when everything is going right, you are probably not going to say
anything. It turns to zero, people just assume it. But that is not good, you want to pay
attention and if your person or your children, wife, husband, whoever, if you want to
rectify your relationship with them, and do not do this in a manipulative way - it won't work
\- but if they do something that is promoting peace and good will, attend to it, tell them
that you noticed. It is so useful, well, you have to get rid of your grudges and your resentment
to do that because you may kinda be mad at that person, and if they do something good,
you may think "there is no damn way I am going to reward it back", so you ignore the people
when they do something good, and well, that is 'truly brilliant' because you have just punished
them for doing what you want. People (going back to my findings about importance of parents)
do this all the time because they let the kids dominate them, then they get resentful,
then the kid will happily run up to them to show them something that is kind of interesting
to them and they will not be happy, they will be like "oh yeah, you know, I'm working",
and the kid kinda slumps down and becomes a all sad and the kid has just learned something
from that interaction, something you do not want your kids to learn. So you have to keep
your relationship with your children spotless and pristine and that means you can't hold
a grudge or resentment against them and that means you have to help them learn how to behave
so that you like your kids. That way, if you like them and you are kind of sensible and maybe
your partner also likes them, so you got a consensus going on, there is a reasonable
possibility that other people will actually like them too, including other children,
and then the world will open up to them. Then you will be able to bring them to people's houses
and the people will actually smile at your kids, maybe give them a pat on the head instead
of thinking "Oh my god, that brat's coming to visit again, I wonder what he will break this
time", and that is just a horrible thing for your child to experience repetitively in situation
after situation, all they learn is that adults have a false smile, but they are really lying
all the time. That's like a bit of Hell and it appears that a lot of children are trapped
in this situation and it is awful to see. I can notice this among the youngest years, in media
and when I visit my old elementary school. When it is among older children then help God, that
is just a horrible thing to witness. And well, you can even see kids like that when you
walk down the street in early afternoon on workdays. Just obnoxious little brats and you look at them
and you immediately want to hate them.

So it is better to not do that. It is better to notice that you are a bit of a monster or
a lot of a monster, and notice that you are much happier with the people around you when they
behave in accordance with reasonable social norms and then you actually feel genuinely connected
to them and you want to work on their behalf so that everything works out. But if you think
you are a good person and that you would never do anything that was harmful to anyone else,
then you can just forget about that because you will never take things seriously enough to
actually learn.

Fuck, I diverged a little again, but this is useful information about relationships anyway.

Finally, what is the ideal person to be in a relationship with? I will try to answer this
both based on psychological findings of people who study this for a living and also what is
my personal preference. Now, the first common misconception people have is that they look
for someone who they will agree with on 100% of things, who just represents the exact same things,
agrees with everything, does not diverge in opinion whatsoever and kinda fits the "perfect
for me bill". However, this is a fool's errand. First off, unless you have been possessed by
a certain idea and find a person equally possessed, then it is hard to find this someone.
And if you do manage to find this someone, then you can enjoy just a short lived relationship
which will come crashing down very soon. This is because according to research, there
are two types of relationships that fail. Relationships where there is more negative interactions
than positive ones, and relationships where there is vastly vastly more positive interactions
to negative ones. It is a surprising fact to learn, but you won't have a good relationship
with your prince or princess charming that you dream of. The thing is, relationships work
when the other person is someone you can contend with, someone who won't just let your flaws
devolve into chaos, someone who makes you grow and opens you up to new things, sometimes
even things you used to disagree with. And the same goes the other way around, they need to
have you as this person as well. Another fallacy is that friendship and a romantic relationship
are mutually exclusive, as some people seem to believe. Well, if you want a short, intense
relationship over perhaps a year, which then fizzles out and ends up dissolving three to five
years later (according to the statistics, it is thereabouts), then sure, go love someone
you are not good friends with as well. And I find it really strange because even if you don't
know anything about psychology, just look at older people. What do you think that romantic
life looks like at fifty? Sixty? Seventy? Romantic involvement requires rekindling every few
years, and if you don't have a good ground to stand on in the form of
a very good friendship, then your relationship will likely fall apart. And you will be miserable,
resentful and you will have lost years of your life. And you can only afford to lose years of
your life to a failed relationship a few times, you fail a few times and you are done, welcome
to the world of not having a family and perhaps just being swamped by cats or videogames.
And going back to the old people. Look at these very old people and analyze their relationships,
they are pretty much just very good friends plus, if you were to imagine young people acting the
same way, you would be like "oh, those are some pretty good friends, nothing else." So do not
have a false view on this topic, and do not also have the mindset of "oh, I will just randomly
date people for fun, I will sleep around and at the first sign of something not working, I will
either leave or threaten you with leaving so you do what I want exactly instead of working towards a solution,
thanks". A very good friend can make for a very good wife/husband/partner. Another thing to consider
is that you do not want the person you are in a relationship with to enable your bad, toxic and/or
self-destructive behavior, but to instead promote your better side. Same goes back, but I think more
people understand this than the prior two.

Now, those are some general things. What would I personally want in a woman? Well,
I have been thinking about this a lot and apart from the three previous things and the obvious,
I wish for a woman who is honest, loyal and truthful. One who shares some interests with me,
but has a plenty of interests I do not know and vice versa. One who has a caring side and yet not
over protective, and also one that I can care about, benefits from my care, but is not fatally weak
on her own. A woman who is smart and can discuss things and hopefully possesses no filters, so even
things most people don't talk about can be discussed. A woman who will contend with me and with
whom I can establish a positive feedback loop, which makes us both grow ad infinitum.
A woman who will understand me and thus cure my loneliness and who can understand my
"will of magnusi" and whom in turn, I can make an effort to understand and provide with companionship
on a deep interpersonal level and can understand her will, that is, her outlook on the world and
what she wants to do about it. A woman who does not need to talk all
the time and we could sometimes just sit at home in a room doing our own things without talking, but just
being happy because the person I love is close. Is this too much to ask for? I would forgo any
notion of looks and even sexual life (in spite of thinking myself to be a person with a sexual drive and open mind)
for this human.

# adskodpsakpodsapodk

Lately, I have been thinking what makes a good friend. I came to the conclusion that a good
friend someone who shares your sense of loyalty, is honest, can be openly talked to and also
is someone you can depend on when tough times come. And someone who won't abandon you at your
first sign of transgression, or from the other side, someone who won't hamper you for trying
to better yourself. A good friend is also someone who is not toxic and who does not want you
to deepen your self-destructive behaviors.

# quit

Thank you all, I have had enough. They have done it, and I can no longer stand it in good health.
I quit, good-bye, pretended to be ill, went home. You know where to find me, but beware, you shall
have no luck in that endeavor until such time arrives that I myself want to be found. Before then,
I shall be absent and unreachable - I have grown weary of people, and I need to take a break. Vale.

# okadkposadpokad

So over the last few weeks, I have been researching the connections of dreams, meaning and myths.
I find it to be a curious topic. As it turns out, we have evolved to sense meaning before having
the ability to articulate it in a factual manner. Imagine seeing a shady person on the bus. You
can tell that they are shady way before you can tell why they look shady to you. Sometimes the
articulation can be even days later or longer. Imagine looking at a painting, you can see there
is something wrong with the painting, but you cannot put your finger on what is it. Until several
seconds or minutes later, when you notice that maybe the perspective is off or something. And why
is that? It is because we have evolved this way to be able to react quickly in situation which require
quick thinking. Like if you are prey to a predator. And now, how do dreams come into play? Well,
Freud had a theory, which has been surpassed since by Jung's, that dreams are the unconscious trying to
convey meaning to us, but that there is an internal censor which prevents articulated information to
be passed through the unconscious - conscious boundary, so the dream has to be sneaky about that,
talking in metaphors, symbolisms and working through associations. To explain, the way you do
psychoanalysis of a dream with someone (Freud invented this and it is still generally in use today,
maybe it is his major contribution to modern western thought), is that you let the other person
recount their dream and you note down the things they speak about. Then you go over through the dream
once more and for each of the things that has been noted down you ask what it resembles, what it means
to them or what it reminds them of. And you piece together these associations and you get the hidden
meaning of the dream, Freud says, quite accurately. Unfortunately, there is a popular notion especially
between my peers and sometimes even therapists, which is frankly appalling, that dreams are of no
significance, or perhaps that they are even random processes.
Now, Jung disagreed on two things, the fact that there is an internal censor and that dreams
are essentially wish fulfillment's (which is what Freud concluded). Instead, Jung discovered and
was able to interpret it in a much better way, that there is no censor, this is as good as it gets,
this is the best attempt at conveying meaning to the conscious that the unconscious can possibly make.
This correlates with the discovery that meaning comes before the ability to articulate it factually,
and this is what it is. Dreams convey meaning as best as they possibly can, and through dream analysis,
we take the raw meaning and we articulate it. That is what's important. How does it connect to myths?
Well, turns out that if you compare the structures of well developed dreams (we are talking ones
that like have some narrative not twenty second nightmares, generally), you will find that dreams are
mythological in nature. They share a mode of information presentation. Piaget and Jung had the idea that
myths and literature therefore must come from the dream. And myths fulfill the same role society that
dreams do to a person. They are raw meaning that unarticulated! It is unarticulated it because it came
to the artists way before they had the ability and the foundation to articulate it! Today, we can
analyse myths that are centuries or even millennia old and we can extract important meaning and moral
messages from them, ones that are in fundamental agreements with what both psychologists and social
scientists discovered themselves in the last decades, and this comes as an amazing fact, because we
can derive one more thing from it. Artists, the ones who create because they must and not for profit
or to try to push an agenda, are the cornerstone of society and the trailblazers of social development.
And so it comes that profound social and psychological meaning is first discovered by artists,
then partially formulated by philosophers and finally completely articulated and researched by
scientists. And look around yourself, this stands true, even the field of psychology itself was heralded
by artists, take Dostojevskij for example, then take Nietzsche and Kierkegaard and many others,
and finally arrive at Freud, Jung and their descendants who based on what artists expressed before
discovered and formulated a field which is now crucial to modern society and understanding of the world!

# operejwpmkkds

A few days ago, Laurens, my brotha from anotha motha, updated me on his relationship situation.
Apparently, he went from zero girlfriends to being between two women, which is a very interesting position
to have. And he is at crossroads, there is one that is very interested in him, is extremely good
at sex and reasonably attractive, but she has a shit personality and there is an air of vanity around
her from what I witnessed. The other one is not interested in Laurens as much at the other and is not
that eager to have him, but she has an amazing personality and she has better predictors for a successful
longterm relationship. And Laurens likes her more. And which one to choose? There is a risk that either
choice may result in the loss of either. I would take the latter one, but for Laurens, there is
a great aspect to consider in terms of "better an egg today than a hen tomorrow". Curious.

# asdpomvsůvlvfssfd

Me and "The Bear" have been more involved in discussions in English class lately. I conclude that most
of my classmates are completely incapable of leading a meaningful discussion. Except for being seized by
feelings, interpersonal relationships and doing the "your facts are opinions and my opinions are facts"
fallacy, arguments ad hominems and so on, they are also guilty of not being able to handle counterarguments.
See, to argument correctly, you have to take the other persons argument and make it as powerful as it
can possibly, you have to really try and look for everything that could make it a powerful argument,
consider all the pros and the details, and then argue with this powerful form. This is the opposite
of a strawman argument, where you cripple and devalue the other argument and then continue to argue with
something that is very disjoint from reality.

# dasopkcsopdkc

I have another game I have been playing for some time. It is called the prediction game. I watch behaviors
and patterns in the people around me and I try to make predictions about what is going to happen, what are
they going to say and what interactions may end up taking place and so on. Turns out that I am pretty good,
it looks like I have chosen well which things to watch for and that I can extrapolate with very high success
the inner workings of people I know and the social circumstances that may take place. Until there is outside
interference, I am usually off only in details. Sometimes, the predictions I make are not particularly
optimistic and not even trying to warn the people seems to work. I wish for these predictions were wrong...

# é=jrewofionvjd

Yesterday, I was coming home very late and I had to walk home a significant chunk because a lot public
transport was asleep already. It was a very surreal experience, since I saw some places that were usually
full of people completely empty, and there was also some strange mist all over Prague. I really liked
how the street lights looked. They had this sort of corona about themselves, it was kind of holy.
There was also a soft wind blowing. It was magical. I took some photos on my still relatively new
smartphone (I am still getting used to this thing, even though it has been a few months), and they
capture some of the magic, but this phone's camera isn't particularly friendly to night time. Shame.
It really makes me want to write or draw something, but I can't formulate what would that be yet.
It's just a feeling at this moment, or an urge.

# aodpkposdvod

Over the last "quitealongtime", I have been involved in a new collective, the IT boys (staff and some teachers)
and I was very surprised by how well read, informed and educated all of them are on things far beyond IT.
They can discuss politics, religion, social things and topics from philosophy at a very high level, which
is really cool. Now, I don't agree with everyone on everything of course, but I believe that makes it even
better, every exchange has been eye opening for all of us, I feel, and I learned things I have not concerned
myself with before. Curious. I like it here, I feel like I belong.

# adsasdpokpoad

Last few months, I have been taking opportunities to consume alcohol at parties, celebrations and with friends.
As a matter of experimentation, I am trying to figure out what does what to me. Turns out that I can deal with
alcohol very well, I feel none to almost no signs of hangover, I am not sick, I don't vomit and I think that
my consumption endurance is well within parameters, I am not a lightweight. An interesting thing is that unlike
many others, I still have pretty much perfect recollection even if I drink so much that I have trouble speaking
and seeing. I guess it's my memory at work again, glad I have it. And it allows me to go back and analyze my and
others' drunk behavior, which wouldn't have been otherwise possible. Pretty cool, I guess.

# rovnice.c

Welcome to the Get Fucked town. This is my solution for a quadratic equation solver program for one of
the classes I am taking. Because I am a shitty prankster, I decided to not only make a performant and
secure solution which ended up being the top 1-3 in ranking, but also to make it incomprehensible and snarky,

```
// program předpokládá celočíselné koeficienty
// vrací 1 při chybném vstupu
// teoreticky vzato má main() jen jeden řádek deklarací a jeden statement
// ~~~~~ INSPIROVÁNO LISPEM ♥ ~~~~~
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

fuj() {
  printf("\npŘeDpOkLáDáMe vŽdY vAlIdNí vStUp\n");
  exit(!0); 
}

main(int argc, char** argv)
{
  int a, b, c, d;
  return ((scanf("%d", 
           (printf("formát: ax^2 + bx + c\n"),
            printf("---------------------\n\n"),
            printf("koeficient a: "),
            &a)
          )
    ? (scanf("%d", (printf("koeficient b: "), &b))
      ? (scanf("%d", (printf("koeficient c: "), &c))
        ? ((d = (b*b - (4 * a * c))) == 0
          ? (printf("x1,2 = %f\n", ((float)-b) / (a * 2)), 0) // <-- 0 je výstupní hodnota při jednom kořenu
          : (d < 0)
          ? (printf("rovnice nemá řešení\n"), 0) // <-- 0 je výstupní hodnota při žádném kořenu
          : (d > 0)
          ? (printf("x1 = %f, x2 = %f\n",
              (((float)-b + sqrt(d)) / (a * 2)),
              (((float)-b - sqrt(d)) / (a * 2))),
            (0)) // <-- výstupní hodnota při dvou kořenech
          : (0)  // <-- sem se program nikdy nedostane
          )
        : (fuj(((((0)))))))
      : (fuj(((((0)))))))
    : (fuj(((((0))))))));
}

```

And they say programming is not art.

# clock.c

Oops, I did it again.

```
// nefunguje, pokud je program spouštěn přes exec(3) s argv[0] == NULL
// vrací 1 při chybě, 0 při správném spuštění - standard garantuje implicitní 'return 0;' pro main()
// viz ISO/IEC 9899 sekce 5.1.2.2.3
#include <stdio.h>
#include <stdlib.h>

main(int argc, char** argv)
{
	unsigned int minuty, vteriny;

	((printf("minuty"), scanf("%u", &minuty))
	? ((printf("vteřiny"), scanf("%u", &vteriny))
	    ? ((vteriny > 60)
	        ? (printf("\nmoc sekund\n"), exit(!1))
	        : (((((0))))))
	    : (printf("\nchybný vstup\n"), exit((!1))))
	: (printf("\nchybný vstup\n"), exit((!1)))); do {
		(printf(("%02u:%02u\n"), (minuty), (vteriny))); while
		((vteriny --> (0))) printf(("%02u:%02u\n"), (minuty), ((sleep((1))), (vteriny)));
		(vteriny = (59));}while ((
		((minuty)) --> (0)));
}

```

It's a clock program.

# oksadppokads

The situation with Ms. Tits (as Laurens calls Sára due to sharing a name with Ms. Boobs)
has come crashing down, unfortunately. The things in her workplace have changed, her mother is now
ill and her school's requirements are even steeper. They have to hand in a 40 page work every month
or two in up to three subjects, she showed me some of them and oof, not easy stuff. She now works
almost every day until 10pm, arrives at the intr at 11pm (she had to get a special permit because
the crazy ladies in there keep calling her mom to discipline her about coming back back late,
even though it is a necessity), then she immediately starts studying and studies until usually
about 2am. I admire her strength, I could not last doing that for more than a few weeks at best.
Unfortunately, she no longer has time for anyone outside her class and she can only message me
late into the night. Shame that she is in such a situation. I hope that everything will be better
once she gets into law school but universities are still a distant (but not so distant actually) future.

# asdokpad

Recently, I have been introduced to the Myers-Briggs Type Indicator, which is a commercial product
which, at risk of being imperfect in many ways and objectively inferior to the Big Five personality
indicator, is an interesting rendition of Jung's personality types. I tried the test on several sites,
to ensure that the results are not biased by a given platform, and it turns out that I am INFJ,
the rarest, loneliest and more depressed type, according to statistics. But what makes me happy
is that I share the same MBTI type with Carl Jung, who has been a great inspiration to me, with
Martin Luther King, likewise, with Atticus Finch and Morgan Freeman. Cool! Most of the descriptions
certainly fits me. Except for the career paths lmao. Well, out of the more common, I could fit teacher,
counselor, psychologist and artist (because programming is a creative endeavor, fight me).
Unfortunately because of the predicament that INFJs statistically seem to have, it is quite
likely that like-minded people, for whom I am looking for constantly, might be greatly struggling
mentally and socially, but that is something I am willing to put up with to the best of my
ability. Anyways, this MBTI thing is eye opening. I might revisit personality indicators later.

# adsadadadadad

For some time now, I have been looking for a work of art, whether it is a book, or a movie, or a
TV series, a painting, anime, podcast, theater play, anything, that could significantly move me.
Turns out some people can be even brought to tears by works of art or feel extremely strong emotions.
Meanwhile I, I spent the last few years making myself as durable and stable as I possibly can,
and I seem to have achieved that goal reasonably well. But appears that in doing so, I have lost
the ability to have fictional things make me feel strong emotions like this. What always comes to mind
is that this is fictional and contrived, and I then handle it as such usually. I have a much better
experience with things created by artists who created because they had to, because there was some
driving force in them to create, spontaneous art, you know? Real life things also have the ability
to make me feel strong emotions, I am not an ice man, I am a somewhat stable and very sensitive and
emotionally driven person (I would say that my emotional side is what drives me towards studying
and analytical approaches, even), but it strange that I became immune to most movies and such.
I think I need to think about this more in depth.

# mmmvmvmvmvmmmvmvmvmv

In the last week or so, I have been examining my musical taste. It appears that it is all over
the place and that there isn't a single genre that could be characterized as a me genre. I have
found dozens of genres in my main playlist, the songs reach from sad to goofy, from slow to fast,
from mild to loud. It appears that, with the exception of game soundtracks, that lyrics are very
important to me, and the meaning they convey. Some of the songs I like have objectively subpar or
basic melodies, but it is the lyrics what make them attractive to me. This being all around the
place is maybe related to me being an INFJ. One of the characteristics of INFJs is that can be
what is called social chameleons. That means that we have a very broad personality and what comes
forward is what is most compatible with the people we are given with at a given moment. This means
that two friends might saw me quite differently because the portion of the behavior that comes
forward in their presence is different. This is not manipulative or a sign of being submissive
(especially since that portion might be the exact opposite to submissive), but a naturally
occurring thing for INFJs. Very curious, I will now try to be aware about this.

# dksdé=púů§-

Once again, I have been thinking about values, virtues and vices. I have been mostly focused
on integrity and love. It appears that integrity is another important virtue a person should
have to be a functional human being that is not corrupt morally. And this is connected with
the idea of leaving your thoughts at the door (like Martin Luther did in a whole different meaning,
also Martin Luther was rampart racist antisemite who really just wanted to kill Jews and burn
synagogues nearing the end of his life), that for true love that you should be willing to leave
everything behind, your moral code and everything. But that is not correct, people who do not have
integrity should not be desirable. This is connected to two other ideas, and people you usually
pick one or the other and end up being miserable. The first is "you should be willing to change
for the person you love", the other "the person you love should accept you as you are". Picking
either of those is a pretty bad idea. Now, what you should do in a healthy relationship is to be
willing to change for the one you love, but without betraying yourself because that will cause
you unbearable misery in the long run, but to also be willing to accept the other person with
their flaws, but that does not mean ignoring the flaws and letting them be unchecked. That is
all for today.

# adspokdokpsa

Guns and deterrence. A strong antigun sentiment is appearing within the radically
politically charged circles, a sentiment, which is completely fallacious in its inception.
The motivation for that seems to be that there is a lot of violent crime, so taking away
guns must make it go down, right? Well, it is not so simple. In the case of US, it turns
out that a lot violent crime is taking place in countries with the strictest gun control,
especially California, which is a state where the politicians just went crazy (for example,
there was a memorial rally for war veterans in California a while back and turns out California
hates it even if you wear your old uniform and gear, not even weapons, so they took all
these poor war-affected men, plenty of them with old injuries and PTSD and arrested them :) ).
It also turns out that vast majority of gun crime is committed with illegal weapons, so if
anything, the correct choice would be to crack down on illegal gun market and gun smugglers,
but that actually requires work and action and the radical Democrats seem to only speak seemingly
virtuous statements and put into effect laws which are "lazy" and do not solve the root of the
problem, or even make it worse. For example, in Australia, when guns were mass taken some
decades ago, there was a massive surge in violent crime which made things worse and set
Australia back several years (there have been a slight downwards trend in crime, taking
guns did a spike upwards and then stagnation, then it started to slowly return to the
previous downwards trend over the course of several years).
Many radically neoliberal types also seem to believe that in US, acquiring guns is very
easy. It is not, I read an article from one CNN reporter, she tried to see just how "easy"
it is to get a rifle. Well, after many attempts, she found out that not very, that there
are pretty sensible background checks and requirements in most places, even in US. She did
not end up acquiring a gun.
Now for the function of a gun. It is true, despite denial from certain types, that guns do
not kill people, but people kill people. A gun won't shoot someone (laws about safeties are
pretty strict, a firearm that can discharge on its own or due to improper handling won't be
certified for sale) on its own and if someone has intent to kill or harm, they will find a way,
gun or not. The primary functions of a gun in civilian capacity is to be a deterrent and
an equalizer. Being a deterrent means that there is much smaller chance of crime taking place
if there is a lot of lawful firearms in a given place. As a robber, rapist or anything of that
sort, you won't go after armed targets. This is why gun-free zones are a bad ideas,
you are literally telling someone "there are no guns here, you will have an easier time
if you go attack this place". And in a more acute manner, if someone tries to do something
to you and you pull out a gun, they will most likely change their mind. Not to mention that
in ongoing crimes, lawful carriers have been known to intervene and helped to defend unarmed
people until authorities arrived. If someone is attacking you, you might not have the time
to wait for police. If not gun, take at least pepper spray, although it is short range,
has limited success and can be countered pretty easily. I wouldn't recommend a knife
because most knifes are too small and probably the attacker, if he has a knife which
is probable still has a pretty good chance of victory. If anything, take a portable hand axe,
that can do similar things knife can while making for a bigger, more powerful weapon.
Not to mention that when in a pinch, most people will have success throwing a hand axe,
whereas throwing knifes is a much harder thing to master.
As for the equalizer part. Having a gun makes muscles irrelevant. If you are ill, disabled
or the perpetrator is much stronger (or maybe there is more of them), then if you or both
parties have a gun, these things become largely irrelevant. Imagine that you are a tiny
woman, maybe like 5'2" and a 6" muscular horny frustrated guy meets you at night looking
to mentally (and maybe physically) scar you for a long time and bust a quick nut. In most cases,
you would have absolutely no chance, only luck. Women are approximately only 50% to 60% as strong
as men in upper body and 60% to 70% as strong in lower body. This means that even at the same size,
most men will overpower women, a 5'2" girl is no match for a muscular 6". But if you pull a gun,
then the mans muscles and your lack thereof lose their meaning. You can now defend yourself.
And if the man then pulls a gun too, then you are on equal terms, and you still have a chance to defend
yourself, especially since you can shoot first.
There is one more thing I would like to mention are silencers. Thanks to stupid politicians who
take their knowledge from Hollywood movies, many countries have prohibited silencers alias suppressors.
They think that it makes just that little boop noise like in the movies, but the truth is very
different. A suppressor does three things: it hides the muzzle flash, increases accuracy and
reduces sound to a level that is not damaging to human hearing, but still very loud. A silenced
weapon is still as loud as a jack hammer. Not just because of the explosion of the gun powder,
but also because once bullet leaves the barrel, it will in most weapons break the sound barrier
which is a very loud crack and you can't silence that at all (actually, since silencers
increase muzzle velocity by lengthening the barrel, using a silencer makes actually more
weapons break the sound barrier, as counterproductive as it may sound). The only option
is to use subsonic ammunition, which travels at speeds below the speed of sound, but that
is not available in all calibers and the gun is still loud. As such, suppressors should not
be forbidden, but mandatory because we do not want to permanently damage the hearing of people.

# asdpodsapoksadpok

Lately, I have been thinking about weak people. I have heard someone on the television say that
showing weakness is good, but truth of the matter is, it is not. Showing vulnerability, yes, but
not weakness, because weak people aren't good (or more accurately virtuous) people. We are talking
weak morally, not physically. Let me outline why. There is a fundamental difference between a person
who has the capacity or possibility to do evil, and yet they choose to do good, and a person who
has no possibility to do evil and so they do good. The first one is virtuous, the second one is
a weak person, and you can be sure as hell that there is resentment brewing within them at their
own inability, and when there is a chance, this creates corruption, and corruption is the farthest
thing from virtue. And this is an old theological question as well about free will and morality:
"Can a person who doesn't have the option to be evil be good?" and I would say no. It is possible
that without the possibility of evil there cannot be good. And we can see this in popular stories
as well. Often the main character has either the same abilities (the same option to do evil) as the
main villain, but chooses to use their powers for good, or they have been touched by evil in a sense,
for example the reason why Harry Potter can stand up against Voldemort is because he has been touched
by evil, and a part of Voldemort's evil exists within Harry, but is has been integrated, domesticated
and the power it has has been used to do good. This is related to the Jungian idea of shadow, a personality
fragment that exists within you which represents your dark side. What psychologist figured out
in the last century is that for a proper mode of existence, one has to integrate this part, not deny
it. People need to realize their capacity for doing evil. And then this malevolent spirit does not
spiral out of control, even better, it becomes benevolent, imagine that. And there is more utility
to it. It is that many things in the world are horrible and you may feel really bad and overwhelmed
by those things and like you are defenseless, but when you realize that there is this power within
you, the capacity to do these things, you realize that you are not harmless and furthermore,
that you can fight back against the terrors of life because of that. According to psychologists,
this is an important realization for many people suffering from certain disorders, and it is such
a drastically important realization that it can apparently even be seen in peoples faces. They say
that their faces harden and that their eyes exude more strength, and aloof innocence disappears
from their expression, and this is one of the factors that makes their life improve significantly.
There is another utility in realizing you are not harmless or 100% good. It is that you realize
and start to consider other people and the possibility that what you are doing may be causing
harm, and so you adjust these behaviors and you end up making the world a better place
and this affects a lot of people as I outlined a very long time ago, given the network nature
of society. This is related to the ideal, which is sadly forgotten by both the radical left and
right (well both ideologies would dissolve if they realized that), that before trying to change the
world and revolutionize society and whatnot, that one should set their own affairs in order. And
just the act of people setting themselves in order helps tremendously. It also helps prevent the
fallacy of "my personal problems require a social revolution".

# iomkjnioplůpúů§.-ú))úůú)ů).-

Recently, I checked out a popular series called "Thirteen Reasons Why". And my question is "why the fuck?".
The characters are horribly contrived, it hasn't seen a real teenager from a fast moving train,
it glorifies toxic behavior and presents suicide as a means of revenge and a legitimate way of
solving problems, while also introducing a romantic aspect to it. This is a really bad message
to convey, especially when Gen Z, the target demographic is the most depressed, anxious, suicidal,
psychologically distressed, lonely and burned out generation with a very long time.
And this is also related to romanticization/glorification of mental illness, the phenomenon of
self-diagnoses and using mental illness as bonus points in the current day identity politics
(as if identity politics haven't been proven to suck by the entirety of last century already, Nietzsche
predicted this even earlier with staggering accuracy). The latter phenomenon leads to more people
claiming they have a mental illness they don't and that is not a personal problem, but a problem
that will then befell the entire body of legitimate sufferers of the given disorder because it will
bring forth misinformation and devalue the weight of the illness. You can already see this happening
with OCD for example, or the bipolar spectrum.

# laurenslol

So Laurens now has a new girlfriend, he met this one in Runescape and she appears to have sunk
several thousand hours into the game. She looks a little creepy and she has unhealthily dark eye
sockets (not makeup) and a pale skin, accompanied by light blonde hair. There is a bit of basement
dweller aesthethic to her, like, I get the sense that she does not care about her looks and appearance,
and I suspect that maybe hygiene isn't perfect either, but I can't smell all the way to Belgium.
She seems to be too clingy and suspicious from what I witnessed and she apparently deals out nudes
like playing cards, which I also find mildly concerning. Given Laurens's personality, I don't think
this relationship will last more than a few weeks, although I do wish him well. I personally would
watch out for this type of person.

# dijs

Three weeks later, turns out that Laurens's Runescape now ex-girlfriend was kinda crazy
and tried to manipulate Laurens pretty extensively, which did not work because Laurens ain't
bitchmade. And this is what I wanted to talk about, manipulating people. I have pretty much
accidentally discovered over the last few years that I have the potential to be a very good
manipulator, I can read people very well, I am a careful people observer and that allows me
to know exactly what I would need to tell them to get what I want, or to get people to like
me, perhaps even feel attracted to me. But the mere thought of doing that feels to me like a
breach of my moral code and my most important values. I think that that should extend to
everyone. I also do not believe that there exists such a thing like manipulation for the greater
good. Moral of the story, do not manipulate people and watch out for signs of being manipulated.

# yxcvbnm

There is a trend in my generation to completely disregard tradition and just consider it to
be some old antiquated bullshit. I believe that this is a very bad stance to take on this
topic. The findings of history are the compilation of what generations and generations of
our ancestors figured out about the world. Perhaps they didn't have the best methods, or they
didn't have the ability to formulate their findings in a factual matter, but it is still a lot
of work. And human life is very short, too short to figure out everything by yourself, so you
need to learn anyway. And even if you decide to take the stance of staunch critic of tradition,
you are foolish to dismiss it. It is one of the most basic truisms that you should know the
things you are trying to criticize, and that you should know your enemy. But I believe that
these young progressives do not take a comprehensive look at tradition on a purpose, out of
fear that they might realize that not all what they preach and criticize has the qualities
they criticize it for. This is very common with the judeochristian mythos, for example. It
is easy to be a young critic, but most of these radical atheists have probably not studied
the texts or pondered the meaning and utility in them. The Bible is an intricate interlinked
compendium of very carefully selected archetypal stories. Very many of these stories have
a profound meaning and bring forth moral lessons that stand even today, that people,
sometimes even the staunch fervent atheists rediscover today, and it is foolish to interpret
these biblical stories in a non-metaphorical manner, wise believers figured out that a very
long time ago. And it is funny when these radical critics associate with Nietzsche, who
had pretty much the opposite stance and, were he to see these people, he would react with
a "what the fuck are you doing you fucking morons, I am probably going to crazy again because
of you all, okay, bye-bye, do not let my sister touch anything I have written thanks."

# pl,mkoijnu

Terraria is slowly becoming less relevant, but I still discover things about the human condition
from it. Through my interactions and admin work for many years (not to mention findings from
outside online as well), I can now create a basic scale of struggling people from worst condition
to non-struggling. Now, there is basic thing to be known from a psychological perspective.
These people are often empathetic and the behavior they experience while struggling mentally
is often affected by their empathy or perceived lack thereof in others. Of course, these
correlate with psychological research, but I am presenting these types in a more down to
earth manner.

- I am struggling, things are bad, I am miserable, nothing matters and I feel like the only way
  to get this point accross is to target others so they feel the same misery as I do. (this type
  of person is also what evolves into the school shooter mentality)
- I am struggling, things are bad, I am miserable and I am bringing about short term nearsighted
  relief by way of engaging in self-destructive behavior such as alcohol, drugs, irresponsible sex
  and so on.
- I am struggling, things are bad, I am miserable and I am wallowing in pity, but not overly
  destructive
- I am struggling, things are bad, I am miserable, but I have found some hope and I am slowly trying
  to crawl out from the proverbial ditch
- I am struggling, things are bad, I am miserable, but I am working on solving the things that cause
  my situation to be as bad as it is
- I am struggling, things are still largely bad, but I have found healthy coping mechanisms and I
  have a much better view of things
- I am struggling, but things are improving
- I am struggling, but things are pretty good already, my condition is a matter of adjustment period
- I am not struggling on the large, but I could use some advice
- I am doing fairly well, I can exchange advice with others, my experience can be considered as largely
  positive
- I am doing very well and I have my life set in order (pretty rare group, but I have met a few and
  consider them to be good sources of advice)

Now, notwithstanding that I don't suffer from any mental issues as far as I am aware, I think that I fall
somewhere in the neighborhood of categories 2 and 3 from the bottom, but there was a considerable time
where it would be about four and perhaps even a short period of five or maybe six. Number one from
bottom is of course the ideal, but I am not sure how long it will take me to get my affairs in such
an order that I would qualify. Curious.

# uiureiuf

During the last few months, I have been trying to learn about women, birth control, biology and
its relation to politics and current day society, and after reading a lot of research materials,
statistics and studies, I learned some interesting facts. Turns out, if you track women through
their ovulation cycle and you show them a picture of the same man, and you do nothing but vary his
jaw width, then when they are ovulating, the guy with the wider jaw is more attractive, and when
they are not ovulating (the farthest away from ovulation), then the guy with the thinner jaw is
more attractive and that is associated with testosterone levels. This means that women who are
fertile like more masculine men. And if you are a woman and on the birth control, then you are
essentially never in the ovulation phase, and this has apparently had an impact on society.
Since women have been taking the birth control, their preference for less masculine has become
more pronounced and that is one of the things that's fueling at least some of the tension between
that exists now politically between men and women. But the more important point is that you just
cannot ignore the massive consequences of a biological revolution like that, and to make any other
causal, when you are trying to understand the political moments in the last forty years or so.
It is like putting the cart before the horse.

Now, it is reasonable to point out that the birth control pill would not have been accepted as
a technology back then if certain political changes regarding to the emancipation of women had
not already been in place. No one would have even been allowed to do something like investigate
contraception, so it is not possible to separate the biological revolution from the political
entirely, but it is still very useful to organize your thinking to realize just how profound
and important a revolution that was.

Back in Victorian era, there is another thing about sexuality that is worth talking about today,
as funny as the proposition may seem at first glance. Modern people like to think that there is
nothing dangerous about sex (and that it can be taken as a casual past time or engaged in
irresponsibly), and that is one of the most stupid ideas one could ever hypothesize. Because
everything is dangerous about sex. It is dangerous emotionally. It is dangerous because of the
possibility of unwanted pregnancy. It is dangerous socially. And it is dangerous because of the
possibility of sickness, and that is one major con to consider. Think back, when AIDS first
came around in the 1980s, it could have easily killed all of us and the fact that it didn't
was definitely part miracle. That it didn't kill us is great, but it did kill millions and millions
of people, it was no joke (and it still kills over a million of people a year, by the way).
And AIDS mutated to take advantage of promiscuity, and so the relation between sexual behavior
and the transmission of disease is actually brought about at the biological biological level,
but back in the 1890s, during Victorian era, they had the exact same problem with Syphilis
and Syphilis is a nasty disease as well. It can mimic many other diseases and it is eventually
devastating to your nervous system, and it can be passed onto children. And so, part of the
reason that sexuality was heavily repressed in Victorian era was not only because of the
possibility of unwanted pregnancy, in relation to the relative poverty of people, since in 1895
in Europe the average person lived on less than a dollar a day, and that is current day dollar,
not 1895 dollar, it is almost impossible to imagine how poor people were. And sex in a
poverty-stricken place is also a lot more dangerous that it is in a rich place because,
especially if you were to happen, given the lack of employment opportunities for women back in Victorian
period, to get pregnant out of wedlock, then you were in serious trouble as a woman.
And so, the fact that sexuality was repressed is hardly a surprised, because it was so difficult
to integrate into the full fledged personality, as it still is.

Now, Henri Elleberger, a Canadian historiographer psychiatrist sums it up as such:
Sexual repression, a supposedly characteristic feature of the Victorian period was merely
often the expression of two facts, the lack of diffusion of contraceptives and the fear of
venereal diseases.

And this was made even worse due to the shape-shifting and hereditary nature of untreated
syphilis, which had become a nightmare for many and to which many physicians attributed
all diseases and issues that they couldn't otherwise identify. "You got this disease
and I don't know what it is as a physician? Well, I am going to tell you it is hereditary
syphilis, enjoy thinking that your life is absolutely ruined and that you have a short
expiration date."

And so it is important to think about the dangers of sex even today, and these were just
the biological aspect. Count in the mental scarring from irresponsible sex and putting yourself
in places where one can get taken advantage of by not being vigilant enough and voila,
the situations can get much worse. And wounds caused by sexual abuse turn out to be much
much harder to deal with than other types of mental wounds.

# wertzuiopú

Recently, I have been interested in the topic of self-harm. For the longest time I could not
understand the motivation behind why do people harm themselves. So over the course of several
weeks, I went carefully around the online people I talk to who used to do it. I had to be very
careful about it, since I did not want to bring forward any old trauma, so I had to take a very
methodically sound approach. Now, what was already clear to me is that it is a coping mechanism,
but what I was curious about was "how is it a coping mechanism?" and I think that pieced together
a pretty interesting narrative. One person told me that there used to be a voice in his head that
would constantly yell at him and belittle him and that it would cause intense emotional pain, unless
he cut himself. This was one of the two men who self-harmed that I had access to, the rest were women.
According to the research, women are more than twice as likely to self-harm, men use other dangerous
coping mechanisms. And although most others weren't as talkative as this one man, I could start seeing
patterns. It is related to the causing one pain to stop another technique. It is a very old discovery,
perhaps even ancient, that if you introduce a new source of pain, the old ones will temporarily stop.
This is a similar principle, especially if the self harm manages to evoke an adrenalin response.
You have intense emotional pain and or trauma, you cut yourself so that for a moment, you have
some chemicals in your system and then for another short period, the physical pain takes over from
the mental one. And this physical tends to be more manageable for these people. Except for a few
specific cases that appear out there in the wild, particularly on Tumblr, I believe that the narrative
of "doing it for attention" is foolish and detrimental to sufferers who feel no other option than to
cut themselves. I find it really curious that mental/emotional pain and physical pain are so closely
connected that you can use techniques that deal with one to deal with the other. Nevertheless,
I think that self-harm is definitely not something to be taken lightly, and the fact that it can
be used as a coping mechanism (although definitely a bad and self-destructive one) should not
ever allow anyone to turn a blind eye to witnessing it in the people around you, especially since
it is an indicative of deeper problems.

# diefjijf

For a few years now, there are discussions about legalizing gay marriage. The narrative
that is presented by the media is that left wing is "yes-gay" and right wing is "no-gay", but the truth
of the matter is that this is not a problem of left and right wing, but of authoritarianism
vs liberalism, the other axis of the political compass. More liberally leaning (in the original
meaning of the word) individuals support gay marriage, whereas authoritarians dislike it. There
is more nay-sayers in the authoritarian right than in the authoritarian left, this is true, but
it is important to look why. For the entirety of right wing, family and raising children are an
important value, and there exists a concern that legalizing gay marriage can weaken the traditional
model of family. However, while this concern is understandable and it is true that certain progressive
policies have destabilised the family a bit (I might go into detail later), a conservative argument
can be made in support of gay marriage, which is of higher value than this concern.
During the last few decades, many studies have been done on the development of children, and
there are things that we now know for certain, they have been pretty much researched to death.
One of these things is that children coming from two-parent complete families are doing infinitely
better in virtually every aspect - school performance, physical strength, health, social status,
emotional stability, mental stability, longterm success, pretty much every variable you can imagine.
And therefore we want to allow gay marriage and gay adoption to ensure that there are more complete
two-parent families (and it seems like it does not really play a big role if the child is adopted),
since it will be infinitely better for the children. Now, there exists a reasonable concern
that in a family with same-sex parents a role model of one of the sex will be missing and that
it may have a some impact (and we know that for the proper development of a child, it is desirable
to have role models of both genders), but so far we do not have data on this and we cannot tell
for sure. But we know one thing for sure - two parents are better than one for the children,
regardless of gender. And if for nothing else, for this simple reason gay marriage and adoption
should be allowed. This is a conservative argument for gay marriage.
One thing I am particularly interested in are the inner workings of a homosexual relationship,
but I need to collect more data before formulating any findings. I suspect that things will work
on some level differently psychologically, due to a different effect of biological predispositions.
There is another point of contention in the gay marriage topic, and that is whether gay marriage
should actually be referred to as "marriage", or not. Some, particularly catholic types, argue
that the term marriage refers to a holy union between man and woman. I am not sure about that.
It appears that the word "marriage" has different etymologies in different languages, and the
different etymologies have different implications, from a linguistic perspective. Therefore
I believe that the perspective and eventual decision might differ from a language family to
a language family, but I do not really know enough about this point, so I am not sure,
and would not like to pass judgement on the terminology, definitely not now. I am personally
fine with calling it marriage, though.

# ndndndndnndn

I would like to briefly get back to postmodernism and why I dislike it for both literary
interpretations and moral implications. The literally issue is that you can take a text
and you interpret it in a great variety of ways. But just stopping at that is wrong because
what a person should be looking for in a text (and also in the world for that matter) is
sufficient order and direction. This begs the question, what does sufficient order and direction
mean?

Well, as a person, you do not want to suffer so much that your life is unbearable,
that should be self-evident. There is an old truism: "pain argues for itself". Pain can
be a fundamental reality because no one disputes it. Even if a person says they don't
believe in pain, it doesn't help when you are in pain - you still believe in it, you
cannot pry it up with logic and rationality. It just stands forth as a fundamental part
of existence, and this happens to be actually a very useful thing to know. And you
do not want any more of pain than is absolutely necessary, that should be also
self-evident. However, one can say it's more complicated than that, you don't
want any more of it that is necessary today, but you also not tomorrow, next week,
next month or next year.

So the way you act now should better not hamper how you
are going to be in a year because that would be counter-productive. And that is part
of the term with short term pleasures and "living in the moment". It is like the old
aphorism "Act in haste, repent at leisure", everyone should know what that means.
Therefore, a person has to act in a way that works now, tomorrow, next week, month
and so on. That means you need to take your future self into account, and humans can
actually do that very well, maybe because of snakes, as I explained earlier. And humans
are maybe the only species that can consciously take their future self into account.
And taking your future self into account is not very different to taking someone else
into account. And we can look at it from the opposite perspective. The you that is out
there in the future is sort of like another person, and therefore figuring out how to conduct
yourself properly in a relationship to your future self is not much different to figuring
out how to conduct yourself in relationship to other people. Then we can expand the
constraints. Not only does the interpretation that you extract from the world protect
you from suffering and give you an aim, but it has to do in a way that is capable of
being iterated, so it works across time, and then it has to work in the presence of
other people, so that you can cooperate with them and compete with them in a way
that does not make you suffer more. And people are not that tolerant, all in all,
they have choices, they do not have to hang around with you, they can hang around
with any one of these other people, and so if you do not act properly at least within
certain boundaries, you are just cast aside. And people are broadcasting information
to you all the time about how you need to interpret the world, you just have to look,
so they can tolerate being around you. And you need that because socially isolated
people tend to go insane and then die. No one can tolerate being alone for any length
of time, we cannot maintain our own sanity without continual feedback from other people.
It is too complicated.

Therefore, one is constrained by their own existence, and by the existence
of other people, and then also by the world. If you read Hamlet and what you extract
out of that is the idea of "I should jump off a bridge", it puts your interpretation to
an end rather quickly. It does not seem to be optimally functional, so to speak. And so,
an interpretation is constrained by the reality of the world, the reality of other
people and reality across time, and there is only a small number of interpretations
in that tightly defined space. That is part of the reason why the postmodernists are
wrong. It is also part of the reason (as a computer nerd fun fact) that AI researchers,
who are trying to make intelligent machines, have had to put them in a body because it
turns out that, in some sense, one cannot make something intelligent without it being
embodied it is partly for these reasons: you need constraints on a system, so that the
system does not drown in an infinite sea of interpretation. That is the literally end
of postmodernism.

For the moral aspect, well, morality, at least as far as I am concerned,
is about action. This is an existentialist view in a sense, and what that means is that
I believe that what people believe to be true is what they act out, not what they say.
And well, there is a lot of definitions of truth. One can think of objective truth,
but behavioral truth is not the same thing as objective truth. What you should do
(behavioral truth) is not the same as what is (objective truth). Well, people sometimes
debate that, but I am a firm believer that has to be the case is because, say, for
example, imagine this.

You are standing in front of a large open field, and you can see the field, but the
field does not tell you how to walk through it. There is an infinite number of ways
you could walk through it. That means that one cannot extract an absolute guide to
how you should act from the array of facts that are in front of you because there
is just too many facts, and they do not have direction, but you, as a person, need
to know how not to suffer, and you need to know what your aim is. Therefore, you have
to overlay that objective reality with an interpretive structure. And we observe parts
of this structure from our behavior and other people's behavior, and we have extracted
part of this by the nature of our embodiment that has been shaped over hundreds of
millions of years but we see the infinite plane of facts and we impose a moral
interpretation on it, and the moral interpretation is "what to do about what is",
and that is related with both security and also with aim.

Humans are mobile creatures, we need to know where we are going because all we
are ever concerned about is, roughly speaking, where we are going, what are we
doing and why, and that is not the same question as what is the world made of
objectively. It is a different question, it requires different answers. And so
that is the domain of the moral, which is "what are you aiming at?", and that
is the question of the ultimate ideal in some sense, even if one has trivial
fragment-like ideals, there is something partially emergent out of that chaos,
it is more coherent and integrated, and more applicable and practical. That is
the other thing. When you think about literature, art, it appears evident that
those are not really tightly tied to the Earth, they are up there in the clouds,
so to speak, spiritual and airy, and they do not seem practical.

And yet, I consider myself to be a practical person (roughly speaking). And part
of the reason I might want to examine works of art from a literary, aesthethic,
evolutionary and psychological perspective is so that I can extract something of
real value that is practical.

Perhaps this what I want to convey in my writing  eventually, that is, something
someone can use, since I think of knowledge as a tool, it is something to implement
in the world. And humans are fundamentally tool using creatures, and then our
knowledge is tools, and we need tools to work in the world. We need tools to regulate
our emotions and to make things better, and to put an end to suffering to the degree
that we can and to live with ourselves properly, to stand up properly. And humans
need the tools to do that.

So, although this was going at it from the side, and it might not be comprehensible
without prior knowledge of the postmodernist stance, the message should be clear:
postmodernism is a bad philosophy to order your life around, and it is a very bad
mode of thinking. It is based of things which are not work and have been disproven,
such as the claim there is nothing such as intrinsic human nature and that everything
is created socially, or that there do not exists truths in the world, that is also
a bad thing to go by. Not to mention the fact of combining things and views which do
not belong next to one another and not really doing anything about it.

And so, adopt responsibility, interpret things properly, make aims for future, plan
ahead, pay attention, speak the truth, do not let mutually exclusive beliefs take
hold in your mind, and look at other people, and let yourself and them work in such
a way that leads to your improvement, and conduct yourself in such a way that leads
to improvement in others. That is my little wisdom for today.

# saddssadadas

Lately, I have been wondering about a pattern that emerges with certain types of
mentally struggling people. It is that they do destructive (we are not talking self-destructive
in this case), damaging or misery-causing actions. The fact that this pattern
emerges is not anything new, really, pretty much everyone can notice and observe
without requiring any advanced skills. What interested me, however, was the motivation
behind this. According to research, there is a number of reasons - it may be compulsions,
momentary relief, or even being so detached from reality that they do not realize the
implications of their actions, i. e. their destructive nature. But there is one motivation
that piqued my interest the most - doing misery-inducing things simply for the reason of
causing misery in others. I briefly outlined this a long time ago in my classification,
but this is related to empathy. Now, there is an old psychoanalytical method (I think Freud
first described it, but I am not sure right now), in a nutshell, it says: "If you do not know
why someone is doing something, look at the results and try to infer the motivation.". That
is, the reason someone may be causing misery is simply to cause as much misery as they can.
Now, before we continue, there is a certain danger to this psychoanalytical method wherein
you may, if you reach for it first, miss the actual motivation, but it is useful if no other
approach works. And now for the big question. Why would you, in a state of misery and mental
woes, want to cause misery to others? Well, it turns out that the reason is empathy. Most of
the people who fit into this category are high in the empathy trait, and in their state of
misery and mental woes, feel like no one can understand them and relate. Even worse, they
may feel like everyone just elects not to notice they are suffering and ignores their issues
on purpose. This is, of course, very often a fallacious conclusions, people are generally
really talented at hiding their struggles from the general population, just look at social
media, so it is not like most people around them even know that there is something going
with them. And the struggling perceive this as something that is personally targeted at
them, that people do not relate to them on purpose. So what they do, based on this perceived
lack of empathy, is to try and cause misery to others to somehow force them to relate,
although this almost never works and just breeds further resentment. When things are
really bad, these people sometimes think: "How could I cause as much misery as is humanly
possible?" and the answer is: "Target the innocent, the pure." That is, the children,
and this is how you get school shooters of the already adult variety who either go shoot
up a random school, or they go to shoot up the school where they studied years ago. This
is distinct from the still studying school shooters, who are primarily motivated by revenge.
They want revenge for all the pain on their tormentors, then they throw in the other students
because they feel like they were complacent, and then they throw in the school staff as well
because they feel like they failed in their job and did not protect them from their pain.
So that is different. And now, going back to the first type of school shooter. Sometimes,
they take what they are doing to the next level and after shooting up the
school/kindergarten/whatever shoot themselves just to really drive in the point that
nothing matters, just misery and death. And so the moral of the story is that people
have motivations for their actions, even when they are struggling mentally and miserable,
even when they claim to be a "random" person and/or appear to do seemingly random actions
(and those are people who are especially not random, when they claim it), and that it is
worth observing what the motivation is, if for nothing else then to maybe understand your
fellow man and perhaps observe what they are dealing with. And how to do that? Watch their
longterm behavior, take into account who they are as a person, their place in society,
the setting, the patterns that you can spot, maybe psychological findings if you have studied
psychology, and finally, the result and try to piece it together. If it doesn't work, fall back
to the "inferring motivation from result" method. Seldom there is something that is truly
random. Humans are fundamentally incapable of doing random acts that would just
emerge from the chaos without any stimuli.

# ertzuikmnbvftzýái

So it appears that during the last decade or so, there is a decrease in marriages and its
perceived value. This is in part because people have started to assign less meaning to it,
dating has been gameified by spastic applications such as Tinder and because dating has started
to be perceived as more of a casual past time, than something you should take serious responsibility
for. What people do not realize is that the increased amount of stories of misery, "evil exes",
infidelity, and relationships crashing down either within half a year or 3-5 years down the line
are direct results of this detrimental shift in mentality. And we know that, we have known these
for years, the research reveals this to be very evident causal relation.
So now, we have pinpointed the first problem - people have the wrong mentality in relation
to relationships. What's next? Well, this leads to inability to communicate properly when it
comes to dealing with issues. People now have a tendency, with the mentality of "just accept
them for who they are and let them have their flaws" (without being conscious about them with
the partner), to wait and wait and not mention things that are problematic for you, points of
conflict. What this leads to is that the anger escalates, you grow resentful and when the boiling
pot finally explodes, it is an all out warfare. And then you are arguing to because you want to
resolve the issue, but because you are letting out anger and you want to take it out on the
responsible party. And in the moment you use the argument "I am going to break up with you/
I am going to divorce you", then you have reached a kind of critical point. Because that is
not negotiation (and all personal relationships are actually forms of negotiation, we have known
this for decades), but threats. And threat is not the optimal way to resolve an issue. Well, and
so the question might be, "what can I do about the things that irk me, then?" Well, come out with
them the moment they irk you and resolve your conflicts at the lowest possible level you can,
that is, for example, let's reach into the territory of what might be considered cliché today,
imagine you want your spouse to kiss you whenever they leave the house, for example, to go to
work. And you get really mad about the fact that they don't do it, and if you let this issue
stay silent for an extended period of time, you might even feel like "does this person really
love me?", and this is not an overstatement, little things can grow into monumental mental
monsters if you leave them unchecked. And so you finally end up arguing and you are like
"well, you don't kiss me at the door, you don't love me anymore, I want a divorce." And the
other person will probably be like "what the fuck" and will start bringing things that irk
them about you, and you will just end up yelling at each other, doing things that you will
maybe regret later and you will resolve nothing. So what you instead want to do is say
"I would really appreciate if you kissed me at the door when I'm leaving", and then
you discuss it. Oftentimes with these tiny issues, you may end up discovering that the
other person never thought about that and will say like "yes! great idea, why didn't I
think of that", or you may end up discussing it and figure out why that isn't the case,
and you may either reach a compromise or you may get an explanation, if nothing else,
and then you know "oh, it's because of that, not because they don't love me".
And thanks to the relative instability and mutability of these relationships, the entire
relationship is threatened by the constant option one party just walking away instead of
resolving the problems. This is because it may seem easier to just say "up yours", leave,
stay resentful and then just enter a new relationship (which would probably end the same
way, by the way). And the fact that this is not a good idea is baked even into the marital
vows: "I am not leaving, ever, no matter what." And that puts a boundary around your
arguments, so now, you can't just walk away easily (of course, there is divorce as an escape
hatch when things just don't work irreconcilably or if an irredeemable act is committed).
Like imagine living with this: "Every time you manifest one of your flaws, every time you
step out of the line, well I'm outta here". That is a horrible condition to live under
and a horrible perspective to have, and that is for both of the people engaged in the relationship.
This is not something you should wish to inflict on anyone, even less so your romantic partner!
And well, if I am going to be stuck with this person, it makes sense that I would want to
make this the most enjoyable experience, so we better do our best to work out our problems.
And well, the method I have outlined, and this is one of the things that a good relationship/couples
therapist should teach their clients very very early on, will of course lead to a plethora
of tiny conflicts, before each of the topics is worked out. But over time, there will be
fewer and fewer of them and the intervals will be shorter and shorter, until you eventually
reach a state where, all things considered, you are satisfied and without this petty type
of conflict. This correlates with what I have said about speaking truth a long time
ago. It is fundamentally the same principle. Relationship do not (under normal circumstances)
collapse because of one decently sized thing, but because of many tiny problems which,
by way of not being dealt with when they occur, grow to gargantuan proportions. And
so, speak the truth and have a responsible attitude towards what you are doing in a
relationship! You cannot just think that things are magically going to be perfect
without being conscientious about your relationship. That is just wrong and humans
have known this for centuries, then come the psychologists and confirm it, and then
came the postmodernist thinking people with an "up yours, I do not care about both
research or the discoveries of our ancestors or the underlying meanings buried at
the core of our tradition, bye bye". Frankly appalling.

# 09876543456789

So I started dating this one girl. She is a somewhat strange person, which I find endearing,
she is very very intelligent and generally highly knowledgeable in a variety of scientific fields,
somewhat like-minded in an array of topics, of a reasonably attractive temperament (in relationship
to mine), and frankly, I just took liking to her. I met her when another professor kind of pushed her
in front of me because she wanted to take my Informatics class, but she had the smart idea of
lamenting this out loud in lesson with this guy, and he basically said that he thinks that I
will take her in anyway, which was a correct assumption. For the first few classes, she was
displaying some signs of strange behavior, so I was very curious about it. She also jokingly
exhibited abysmal self-esteem and most of her humor was self-deprecating, which I took as a red
flag. Eventually, I managed to speak to her alone one day, and got her to open up to me. And you
can do this pretty easily, it is like a straightforward, ethical technique, it involves building
up trust and sincerity and opening up yourself. And what she told me was quite horrible. She was
deeply depressed, had delusions, was hearing voices who kept threatening her and saying terrible
things, kept seeing abusive apparitions in her mind, had pretty much zero self-esteem, she felt like
she did not fit anywhere, she was self-harming, she contemplated and apparently attempted suicide,
she felt deeply lonely and misunderstood and she was full of pain, trauma and resentment. This was,
in its inception (and hers as well not incidentally), due to her parents. In the eyes of her parents,
this girl's (whom Laurens calls either Ukrainian Girl or Ukrainian Redhead) existence was a mistake.
Her father was a rich business man with a big company that had a large area of influence. Her mother
was an irresponsible gold-digger floozy, who had a dream of getting herself into England and having
a comfortable life there. However, these two people had an encounter at a party once, when her mother
was only about 20 years or so old. The result of this encounter was Ukrainian Girl. And so there was
a lot of resentment because of her, the mother had to stay here in Czech Republic, and the father was
none too happy about being stuck with this type of woman. And the bone of contention? Ukrainian
Girl. So she got the brunt of it, pretty much a lifetime of abuse at the hands of her parents,
especially her mother. This was coupled with strange beliefs that her parents had, including a
distrust of doctors, psychologists, glasses, medications, research and proclivity towards
conspiracy theories and strange religion stances (her father decided it would be a good
idea to combine orthodox eastern Christianity with Hinduism, for example), led to Ukrainian girl
having essentially no leg to stand on socially. This is made even worse that the fact that she
looks very much like her mother, and her mother was jealous that there is a younger, fitter
version of her in her vicinity. In essence, she sees her daughter as competition. These were
all heavy discoveries. Well and my goal, in light of this, was to do everything in my best
ability to help, and to get her to go to a psychologist and get some mental help. And well,
she was very happy to have someone like me. Whenever she was distressed on in a very dark
place she would call me and I would listen, provide compassion and then speak about how
I see the topic, what would I recommend and what is the best way to go about conducting
yourself in the world, or perhaps more accurately, how to reason in such a way that you
can discover the optimal mode of being in the world. Each of these sessions was hours
and hours, sometimes up to 4am or once even 5am - she had completely fucked sleep schedule
and I can handle some beating - and eventually, I started seeing progress. However, seeing
a psychologist still has some obstacles, namely her parents, they have indoctrinated her
with a deep distrust towards these specialists and let her to believe that this won't help
anyway. And that they won't let her go to a therapist. So this is still to be seen.
Another things that she started calling me about were relationships and interpreting other
people. I believe that there is maybe an Asperger's element to her, or another disorder
which impacts ability to perceive and interpret others' behaviors and emotions, and so
she tried to invent ways of dealing with this. These may sound a bit funny, but what she
would do, and I advised against that, was filling out psychological tests, personality
indicators and such "as" the people she wanted to make sense of. However, due to her
predicament, filling out ten tests for ten people did not get her results of the ten
people, but of Ukrainian Girl times 10, but with different moods. For example, a test
she did for me was plainly wrong straight from the beginning because I am not an
extrovert. And my introversion is a pretty significant trait of mine, I am very introverted,
although it does not mean I do not know how to conduct myself in a social setting. Well,
and what I would do is take apart the personal relationships matters she was concerned
about, often times it was drama between two or more of her friends, and we would pick
it apart. She, just like many other mentally struggling people I have spoke to in the past,
has (but this has since drastically improved) a penchant of almost invariably coming to the
wrong conclusion. This is underlined by another typical trait of mentally struggling people,
fatalism. Every time two of her friends were in conflict, she had an incredibly glum and
pessimistic outlook on the matter at hand, she would think that things are bad, and that
it will stay like that and that it is inevitable that everything will be terrible. Every time,
I would do my best to explain that that is not the case and that people can reconcile, and
that minor issues between people are normal, that they will be talking again soon. Most
of the times, I was right. Then during December, I learned that she never had Christmas
or a birthday celebration (she was born during Christmas). So me and boys from the class
got together, procured some shit, got a gift, a cake, candles and sparklers, some chips,
chocolate and other stuff, and we went over to her home, the address of which I have
procured surreptitiously. However, it was a panelák, and I did not know the floor she
was living on. I called her and asked and she told me the wrong floor. When we found
out that she was lying, I asked her if she was in the flat Neighbor A or Neighbor B,
at which point she finally realized we were actually in the building and divulged the
actual floor her family's flat was on. When we got there and she saw the cake, the
candles and so on, she started crying and trembling and then hugging all of us one
by one, to the chagrin of The Polish Guy. Anyways, I spent a lot of time in the days
after that, we spent a lot of time on walks through night time Prague and also going
to the cinema and/or food. Eventually, we had a strange moment in the subway at 2am
and that's how it happened. However, I do not think it is going to work in the long
term, her problems are too extensive, her emotions are all over the place. Until she
gets proper medical care and her parents get the shit kicked out of them, I think she
will (and she does) have trouble with any sort of relationship.

# yiiiiiiiiiiiiiiiiiiiik

Some time ago, I have been acquainted with the game YIIK (stylization of Y2K, the name for
the computer error and overblown cause to worry about societal collapse). I think I should
mention a fun fact about the real Y2K. The problems stated that due to way that before year two
thousand computers only used to store year as the last two digits (well, unless they already
used UNIX time, which the entire date saved as the number of seconds since 1.1.1970, a much
better system). The concern was that when 2000 rolls around, computers would thing it is 1900 instead
and everything would shit itself, computers will crash, society will collapse and everything
will just go to shit. Now, this was blown out of proportion (nothing happened except for a few
limited incidents like a guy being charged about 100 years of phone time for a Silvester call)
by out of all people antivirus companies. They wanted to crank up the sales of their software
so they just kept scaring everyone into buying their shit saying it will proof their computer
from Y2K issues and exploits. Now for the game. YIIK calls itself a postmodernist RPG and it
sucks dick. Just like most postmodernist things, it is not very good. Postmodernism is
a strange thing, very hard to make something good out of it. Sometimes people adopt
postmodernism as their mode of thinking and this will only lead to ruin, since it allows
you to accept without questioning two stances which are in conflict with each other.
In essence, this is like doublethink, instead of the state imposing this upon you, it's
just your dumb ass.

Now for the game. The protagonist is an unlikable dipshit who makes zero personality progress
during the game, people just randomly like him despite him being a huge dick to them (one
of the other characters' father died and the main character had really shit comments about it,
for example). The story mixes so many things that shouldn't be mixed, the game is buggy,
gameplay is unbalanced and uninteresting and the world-building is absolutely incoherent.
The graphics are pretty nice though, I think.

Also the developer is a massive condescending prick, who cannot respond to critique.
When people told him that the unlikability of the main character may have been too much,
he went off on an angry a tangent about world not yet being ready for artistic storytelling
games and characters who are not goody-two-shoes. I think he needs a lesson in recent
videogame history.

Moral of the story: keep postmodernism out of your thinking and be careful about using
it in your artistic expression. I spoke about it before, yes, but it feels like this needs
to be rehashed.

# čšíéporelkfd,cx

Psychoanalytics. Recently, I have read about two seemingly conflicting psychoanalytical
ideas, well these are also very old, so maybe it might be in order to call them mythological
as well, as in one form or another, these have appeared in a number of myths. The first
idea is, roughly speaking, that "there are times in your life when you have to identify things in yourself
that are insufficient, or there is a problem that you have to deal with, and you have to,
let's say, discard/let go this part of yourself that does not fit or is not working",
and the other idea is best formulated in terms of Jung, and it is that "when you become
older, you mature by reincorporating/integrating things that you lost when you were younger,
or that you are integrating your shadow, or other parts of your personality that you have
been rejecting". So on one hand, if you identify a problem, you may want to burn it off,
but on the other hand, the path to becoming stronger is figuring out how to put everything
together. But I believe that there is a way to reconcile these ideas.

So, one of the things that Jung wrote in his works about Alchemy was an explanation
of the prime alchemy motto, which is "solve et coagula", that is "dissolve and integrate".
Now, imagine that you had a fairly hostile father (mine seems that way sometimes but I do not
for a second believe he is), a fairly hostile father who is a decent person does not
control his aggression very well. Your reaction is "I'm never going to be aggressive",
and this makes you build a moral structure, that's a part of your personality, and there
is possibility floating around outside of that you have stripped the idea of aggression
of any ethical utility whatsoever. Now, what happens is that this burns off and then that
comes back up (maybe even with a vengeance) and now you have to integrate it (if you do not want
the trait or lack thereof to cause issues very soon). This is associated in some sense with
Nietzsche's idea of morality as cowardice. This was one of his most sharp critiques of traditional morality,
and the idea is that most of what passes for morality is not morality, it just cowardice.
It is not that "I am a good person and I do not hurt you", it is that "I am afraid to hurt
you and because I do not want to admit that I am afraid to hurt you, I say I am moral because
then I can mask my essential fear and cowardice in a disguise of morality."

This happens far more often than you may think because harmless and moral are not the
same thing at all. Freud said on this topic something to the line of
"the hyper-simplified morality stops you from tapping into recesses of your psyche". And this
is partly because some of the things we often consider dark or problematic like aggression
or sexuality are primal forces. It is not surprising that you do not want anything to do
with them, that you stay away from situations where they might make themselves manifest.
But the problem is that by denying the worst in yourself (and this is also something we
have known for a long time, I mentioned it when I wrote about heroes a while back) or
suppressing it, you preclude the possibility of the best because no one can be a good
person without integrating their capacity for aggression.

This is because without the capacity for aggression, you cannot say no. No means,
if you really say it, "there isn't anything that you can do to me that will make me
change my mind" or, conversely, it means, "I will play for higher stakes than you will".
And unless you have got your aggression integrated, there is not a chance you can say
that, and if you did, no one would take you seriously because they would know it was just
a show.

So, one of the most useful things that Jung did was to work on this idea of the integration
of the shadow because he was really interested in the idea of evil. Especially trying to
work out what happened in Nazi Germany, especially during the second world war. What do you
do with the part of you that is aggressive and potentially malevolent? Do you just crush it?
That is the super-ego response, you just put it behind you, so to speak. Is that a possibility
or do you admit to its existence and bring it in to the game?

For Freud morality was in some sense super-ego clamping down the id, and they were fundamentally
opposed. But Jung and Piaget had a different idea, one that with research that followed seems
more plausible, and it was like "No, no, you invite the bad guys out to play". And so,
imagine that you are an aggressive hockey player, for example. Hockey is a tough sport,
favorite of my brother, and it looks like the players crash into one another quite hard.
Anyways, you are an aggressive hockey player, but it is disciplined aggression that gives you
access to a whole source of energy you would not otherwise have.

And then with regards to sexuality, it is like, well, unbound promiscuity does not constitute
a virtue but neither does unavoidable virginity. In fact, unavoidable virginity might be even
worse, because it also masks itself with virtue.

The fundamental idea is that you should be able to do things that you would not do. And that
is the definition of a genuinely moral person - they could do it, but they don't. That is not
cowardice. And so what you need to do is burn off things that get in the way of the integration
of the whole spectrum of your personality.

One final thing that I ponder about is the quote from Carl Jung: "I would rather be whole,
than good." And that is the essential idea I think. Strive to be whole, strive to integrate
your dark side and all the aspects of your personality that you think lost. And when you do
this, when you recognize yourself, and you speak the truth, the good will follow, it will
emerge out of the system. And you will then be a moral person because you have conquered
the adversities in yourself, your dark side, and aspects of your psyche that are hard to
deal with, you became whole and now you choose to do good, and that is what's moral. It
is the choice, not the action itself.

# asdfhjuztrew

Unfortunately, the last of our Terraria servers closed today. We are now disembodied remnants
of an old community. It was nice while it lasted. Sadly, Terraria is not that popular for server
multiplayer right now (at least not until another big update comes in, in a few years), and most
of the crew has slowly but surely moved on. But with my most important people, I still keep in
touch. Laurens of course goes way beyond the scope of an online friend (he now has another girlfriend,
by the way, met this one on a random skiing trip), but I also got Isaac, my other main Terraria friend,
and Lord Goulash, he is also a pretty cool guy. He is very smart and he imparts a lot of medical
knowledge to me, and he tells me interesting things about anatomy and biological processes, but
sadly, he is homebound right now due to severe clinical depression. Slayer has unfortunately disappeared
from the face of Earth. Jewsus went crazy a year or two ago, he completely lost his marbles after a tough
break up with Nalah, who is my original terraria "boss". Unfortunately, Jewsus did not really want to let
go of his basement dweller mentality, and Nalah, being in the last year of psychology in college
and also a very perceptive and socially oriented woman, figured out that this might be an issue.
I originally served as a mediator between them, being a mutual friend, but after negotiating good
relations between Nalah's and Jewsus's server, I figured that there was nothing more that I could
do. It's a shame, really, I wish that Jewsus would pull himself together, but it may take years,
if it will ever happen. He should probably start by not drinking so much and smoking so much weed.
Then probably try to work through his unbridled anger (and he always had a sort of anger issues,
especially when he was drinking) and his soul-devouring resentment. Bert, an old friend of both
me and Nalah, and as of late Nalah's love interest, has finally finished his navy training and
is now a Navy SEAL. Sadly, he has been immediately sent on deployment somewhere far off and I haven't
had contact with him for months. Hopefully, he is okay. I hope that one day, I will be able to bring
most of the gang together, once again.

# ewroiuip

Sadly, I had to step away from Ukrainian Girl as I expected. Apparently, the voices in
her head have been saying terrible things about me and tormenting her when I wasn't there. Therefore,
I don't see any point in prolonging this torment. It's a shame, despite all of the shortcomings,
it was a pretty nice time and a very profound experience. However, it was at least possible,
through help of two mutual friends, to force her to finally seek mental help, and the school
psychologist now knows what is going on. She had me provide some information about Ukrainian
Girl, especially since during the first few sessions, she had a very obvious penchant for lying
apparently. However, I have not divulged any secrets I was sworn not to tell anyone, even if some
of the thoughts that she told me might have been beneficial in ways of therapy. The secrets die
with me. I feel hopeful for the future, but also, a little bit lonely, I wish some things were
a bit different.

# cmylkcyxcgoodbadshit

So there is this modern idea, that I have been thinking about lately, that you are supposed to just
accept yourself. I think that is an insane idea. Actually, I cannot think of a more nihilistic idea
than that "you're already okay". The answer is like "no, you are not", and the reason that you're
not is that you could be way more than you are. So what do you want to be? Do you want to be okay as
you are or do you want to strive towards what is better? Now, there is this book called "Zen and the
Art of Motorcycle Maintenance" that I find fascinating. It is a Moby Dick type of book, where there
is plot, yes, and perhaps you can read it because you like whales and action, but it is the thoughts
behind it and the explorations of ideas which make it the great literary work that it is. And the
author of this book, Robert M. Pirsig, was a philosopher, he only died recently, and his most important
contribution, I think, is that he laid out the notion that you could make qualitative distinctions, and
he did that in a very thorough and profound manner. And there really was a difference between good
things and bad things or great things and evil things. It gives you direction. It gives you the
possibility of moving upward. And there is a notion pointed out by other thinkers, for example Ratzinger
(as much as I dislike his views on some other things, especially regarding returning to orthodox catholic
values), that human beings are insufficient in and of themselves and need the movement upward. They
need to conceptualize something like the highest good and then to strive for that. And the thing is
that there isn't any difference between conceptualizing the good and being judged because if you're
going to conceptualize the good and move towards it, what you have to do is separate from yourself
all those things that aren't good and leave them behind. And one of the things that's really appalling,
I think, about our modern world is that we are rejecting the notion of qualitative distinctions.
You say, "Well, we don't want to hurt anybody's feelings by saying that one thing is better than another!"
It is like okay, fair enough, it is not fun to be cast off with the damned, that is for sure. But if people
are in fact insufficient in their present condition, which seems to be the case, well, try finding someone
who is not, then if you deny the possibility of qualitative distinction because you want to promote a radical
egalitarianism, then you remove the possibility of redemption because there is no movement towards the good.
And it seems to me that it is a catastrophe to sacrifice the good for the equal because for us to be equal
would mean, as far as I can tell, that we would all be equally unredeemable and miserable. And so, one cannot
just accept themselves. They should not hate themselves, sure, and they should come to terms with themselves,
but do not for a second think "I am as fine as I am, I do not need to improve". You will stagnate, you will
die in a metaphorical sense, and you will became miserable.

# iwodnsklcmxyijosdajdsaoidjsaoidajsdioisadjsaiodoij

Lately, I have been having this one strange dream, an evolution of an older dream or vision.
I in the body of magnusi am traveling to a very distant future. It is a future millions of
years ahead. The Earth is in ruins, the sky has a color which goes from red to dark green.
The temperature is insignificant, maybe like a colder summer day or a warmer spring day.
There is a soft-breeze. The entire landscape is just ash and soot from civilizations past.
There is no one, humanity is gone with no explanation as to what happened. I, as magnusi,
ponder what happened. Every time, I also wonder, "where is magnusi in this future, is he
dead?" or "was magnusi killed during the event that turned the Earth into ruins of soft
dark grey and blue-ish soot?" or "was it perhaps magnusi who caused this event". I am trying
to figure it out every time. Sometimes in my daydreams, I take someone else to converse with
them and show them this future that I am trying to prevent. But lately, a new thing has
happened. I, as magnusi, discover a single man living in this far dystopic future. He is
an old man in simple clothing, with gray-whitish hair and beard and very very light-blue
eyes. I always think: "He is not stained by the ages, it is almost as if by getting old
he regained his purity, as if time moved backwards for him in some sense". And just looking
at this man and his expression tells you one thing: he is a knight. And so, this old man
is called The Last Knight on Earth. And he converses with mag, and he knows what happened, but he
does not want to say. He handles mag strangely, as if he knew who he was beforehand. And
mag tries to figure out what happened and why the man won't tell him, but the man asks
what does he get in return. The last knight on earth seems to have a solemn duty in this
place and he won't leave, he must stand his watch and uphold his knighthood, even though
everyone else is gone, so eventually mag offers him friendship as the one thing he may be
missing. The old man accepts.

# asdopkopv

Recently, I have been interested in creativity and creative people. I am myself a creative
person, I think, and except in the fields of programming and maybe inventing some fantasies,
I feel like my creativity is underused, in particular because I feel like I have no person
to bounce my ideas off, especially since many of them are like really private and personal
to me, and so I used to not see a reason to put them "on the paper", so to speak. But it
appears, or well, psychological research suggests, that the worst thing a creative person
can do is to not be creative. Because then they just die. You can think about it like this:
You are a tree and you have a few major branches, that is your personality. So for example,
if you are extroverted, well, you cannot be cut off from people because you will just wither,
and if you are agreeable, then you have to be in an intimate relationship or you die. If you
are conscientious and you are unemployed, you are just going to devour yourself, because you
have to have a duty and you have to carry a load because you just can't stand it otherwise.
And open people have to be creative, they have to be because otherwise they die, they don't
have any vitality, and so they are cursed with the necessity of putting a foot out into the
unknown and making sense of it, and they are also cursed with necessity of trying to make
a living while they are doing that, which you often cannot because it is almost impossible
to monetize creative action, it is very frustrating for many. But it is not that creative
action were without value because the creative people are entrepreneurs and they revitalize
cities, and the make things magnificent and beautiful. Just look at what's happened in Europe
in the last 2000 years, there is this amazing collaboration to make things so beautiful that
they are jaw-dropping when you walk into them. And you think about the economic value of that,
and well, it is, if I recall correctly, France which is the most visited country in the world.
There might be even more tourists visiting in a year than there are citizens in France according
to some statistics. And a part of the reason for that is that it is just so beautiful that
you cannot stand it. So you think "What's the economic value of that?": it is absolutely
incalculable, what is interesting too is that you build that beauty in and then the farther
away you get away from it in time, the more valuable it becomes. The value of art increases
with time, instead of decaying. And so, trading and partaking in true art (and not things
that are contrived for profit first or to push a political agenda) is invaluable because it
opens your eyes to the domain of the transcendent, even better put, a real piece of art is
a window into the transcendent. And we need that in our life because we are finite, limited,
and bounded by our ignorance and our lack of knowing, and unless you can make a connection to
the transcendent, then you will not have the strength to prevail.

# iusaijasdoil, moů

alternative error handler

```
use std::process::exit;

pub trait Rust<T, F> {
	fn rust(self, F) -> T;
}

impl<T, E, F> Rust<T, F> for Result<T, E>
	where E: ::std::error::Error,
		  F: Fn(E) -> ()
{
	fn rust(self, f: F) -> T {
		match self {
			Ok(s) => s,
			Err(e) => { f(e); exit(-1) }
		}
	}
}

impl<T, F> Rust<T, F> for Option<T> 
	where F: Fn() -> ()
{
	fn rust(self, f: F) -> T {
		match self {
			Some(s) => s,
			None => { f(); exit(-1) }
		}
	}
} 

pub fn e<T: ::std::fmt::Display>(e: T) { println!("doesn't rust: {}", e); }
```

# asdffizutrewqqqqqqqqqqqqqqqq

feed with poetry to generate worse poetry

```
extern crate regex;
extern crate rand;

use regex::Regex;
use std::collections::HashMap;

fn main()
{
	let poetry = include_str!("kytice.txt");
	let word_re = match Regex::new(r" +")
	{
		Ok(r) => r,
		Err(_) => panic!("something went wrong"),
	};

	let words_vec: Vec<&str> = word_re.split(poetry).collect();
	let mut words = words_vec.iter();
	let mut transition = HashMap::new();
	let mut keys = Vec::new();
	loop
	{
		let word1 = match words.next()
		{
			Some(x) => x,
			None => break,
		};
		let word2 = match words.next()
		{
			Some(x) => x,
			None => break,
		};
		let word3 = match words.next()
		{
			Some(x) => x,
			None => break,
		};

		transition.insert((word1, word2), word3);
		keys.push((word1, word2))
	}

	let mut current: (&&str, &&str) = keys[rand::random::<usize>() % keys.len()];
	let mut third = transition.get(&current).unwrap();
	for _ in 0..100
	{
		print!("{} ", current.0);
		current = (current.1, third);
		third = match transition.get(&current)
		{
			Some(t) => t,
			None =>
			{
				current = keys[rand::random::<usize>() % keys.len()];
				transition.get(&current).unwrap()
			}
		};
	}
}

```

# .,,.,.,,.,.,.,.,.,.,.,.,.,betrayal

Lately, I have been thinking about the implications of betrayal and I was interested in
what betrayal does psychologically. Especially, since it seems that many have nowadays
forgotten the weight of promise and do not seem to care if they do not uphold them, or
if they betray someone. Well, I believe that betrayal is a terrible thing to inflict both
on yourself and on someone else. See, If you betray me then I have to see you differently
and you know we have interacted a long time. I've built up a hell of a model of you, which
has take a tremendous amount of effort to generate and I may have used that model as a
predicate for all sorts of things, which is what you do with an intimate relationship. And
so then if you do something that indicates a true mismatch it is not only that I have to
adjust my actions (and sure as hell I am gonna. Have to retool, so to speak). I may even
have to read two of my perceptions of myself: "I am a lot more gullible than I thought I
was, for example" and god only knows what the implications of that are if you are close to
me, and you could do this to me. Is that my flaw and environment am I carrying that into
other relationships? It is an absolute catastrophe.

# tttttttttttttt

This year, I have left school three weeks ahead of everyone to be with grandma in our
summer house. But, this summer is not turning out to be very lonely at all, there is
one girl that constantly messages me and keeps me company, so to speak. Laurens calls
her Minion Girl, since we share a degenerate sense of humor with cursed pictures of these
little yellow shits. I consider her to be a great friend and much better confidant than
almost anyone who came before her, maybe except "The Bear". Minion Girl is a former
friend of Ukrainian Girl, actually one of my two accomplices, but she seems to be
largely healthy in all aspects. She shares a great portion of my world views and just
like me, has virtually no filter for what can be considered too vulgar humor, which is
great. Minion Girl is extremely social and extroverted, which is however sadly to the
point that certain parts of her class reject her and for many things, she finds herself
hovering outside the various circles that have formed there. She is not without flaws,
however, she is a bit too angry, she claims nihilism at times, and she finds a lot of
people annoying even for little reasons. I believe that she has a crush on the other
mutual friend, but does not want to admit it. Let's see if I am right. She is also
very sensitive and things sometimes make her sad, so I had to console her sometimes.
But overall, a splendid person, also on the smarter end of the distribution (to be
honest most of the people that appear in the places where I commonly shuffle about
are smart), but just like me, she is more selective about what she does and does not
do, instead of trying to have perfect grades in everything. Very cool, glad I have her,
she is a great friend and long have I yearned for understanding. I am happy.

# pskpskpkspks

So I did a big brain think and thought about this journal. What I have written here,
except for the times when I pasted code I wanted to preserve in a greater capacity
because I found it funny, is largely my experiences, dreams, compilations and
interpretations of psychological phenomena, sometimes even my own observations.
In general, I consider this to be very personal stuff, the most personal I have ever
written, in fact. There are far more personal things and many other thoughts that
exist in my mind, but I find it too difficult to write these down. I also find it
difficult to convey the emotional message many of these ideas and experiences have,
which may make me seem unemotional at times, which is not true. I think that emotions
play a great role in regards to my personality, and that they are largely the driving
force behind many of the things I do. Nevertheless, this journal is still somewhat
dangerous in that he, who wishes to harm me and gets his hands on this, will now
know exactly how to do that. Still, I think that this will likely not fall into the
wrong hands easily, since I have hidden it well within my computer stuff, and since
I am writing it in such a format and form that most people won't be able to open
and read this file.

# eeeeeeeeeeeeeeee

Jung had this that people's shadows reach all the way down to hell, which can be a
very scary concept. What he meant by this is if you take a look at the impulses that
drive you that are actually malevolent (if you can admit to such impulses, that is),
and if you follow those all the way down to their origin, you find some very nasty things,
and what you find down there basically is what allies you with people who have done
terrible things. And that is not a very pleasant experience, I would say, although
one thing that's worth thinking about is that it is something that can protect you against
being very very badly hurt. Because one of the things that characterize people who
develop PTSD is that they are often naive and then they encounter something that is
really not within their framework of thinking, and it is usually something bad and because
there is not anything in their philosophy (their way of looking at the world, so to speak)
that has prepared them for that, they end up fragmented and devastated. And so it is
actually protective to you if you can figure out what your full range of capabilities is
because that can help you understand other people a lot better, and to be wiser and more
careful in your actions. It is also useful if you want to convince yourself to act properly
because if you regard yourself as harmless (which is a big mistake, I think I already
outlined that before) then nothing you can do is really that bad, right? Because you
think yourself harmless, after all. But if you understand that you are seriously not
harmless, then that can make you a lot more careful with yourself and that is especially
true maybe when you are dealing with your kids, if you are a parent. And this is
backtracking to the immense impact of parents on their children that I am witnessing
everyday. So, if you know what you are capable of, then that can motivate you to be
much more careful with what you say and do. And that does not mean like cautious or
timid. It just means that you want to keep your things clean and pure with your children,
because that way they are on your good side. And you want your children to be on your good
side because children who get on their parents' bad side suffer very badly for it,
and sometimes it is because they are literally abused, but more often it is because
they get abused and neglected in much more subtle ways, and you are definitely capable
of that. All you have to do is think about the way you have interacted with someone
you have decided to not like, or maybe someone you genuinely don't like, and that can
range from just not paying any attention to them, especially if they are doing something
good, to really pursuing them and making their life miserable, and you can certainly do
that with your family members as well, and you can do that with your intimate partners,
and you can do it with yourself, and so it is really worth knowing that. There is a quote
from Jung about this, that I like: "No tree can grow to heaven unless its roots reach
down to hell".

# naziiiiissss

Now, I am coming back a few days to add something of value to my previous entry in this
journal. There is a book, and it is quite good from a psychological and sociological
perspective also. It is called "Ordinary Men: Reserve Police Battalion 101 and the Final
Solution in Poland", which is a very long and descriptive name, and it is a true story about
a German Order Police (Ordnungspolizei, not to be confused with Gestapo), which was responsible
for the mass shootings and round-ups for deportation to death camps of polish Jewish people.
It is a story about these German policemen in early stages of World War II and, these were
guys who were old enough to be raised in Germany before the hitlarian propaganda came out
in full force. Because if you were a teenager in 1930s for example, you would have been pulled
right in into the propaganda, maybe you were a part of the Hitler Youth as well, and well,
you were raised in that, but if you were older, then you were raised before that and once
you are older than about 22-25, you are not as amenable to propaganda, it is pretty young
actually. If you want to make a soldier, you have to get a soldier young because once people
are in their early 20s, they already have their personality developed. Anyways, these policemen
were sent into Poland after the Germans marched through. This was during wartime and there was
this hypothesis in Germany that the Jews in particular were operating as a "fifth column" and
were undermining the German war effort because, of course, the Germans blamed the Jews and a
variety of other people for nearly everything, and of the things was setting up the conditions
that made the war necessary, and so when the police were sent into Poland, they were also
required to "make peace", so to speak, and so they started by rounding up all the Jewish men
between 18 and 65 roughly, and gathering them in stadiums and then shipping the off on trains,
but that is not where they ended. They ended in a very very dark place, these guys were going
in the field with naked pregnant women and shooting them in the back of the head by the end
of their training. And what is really interesting about that is that their commander told them
that they could go home at any time, so this is not one of those examples of people following
orders. And the reason they didn't, roughly speaking, is that they did not think it was
comradely to leave the guys they were working with to do all the dirty work and run off.
And that is a really interesting fact because in different circumstances one would not
think about that as reprehensible, but as part of good teamwork under rough circumstances.
That is, at least in part, how they viewed it. They were also made both physically and
psychologically ill multiple times by the things they had to do, but they kept doing them
anyways. So it is one step at a time. And that is the moral of the story: you end up in
very bad places one step at a time, so you got to watch your steps. And you cannot think
you are just harmless because many of the Nazi offices thought the same thing, like the
"I am just an accountant", for example, and in some sense they were. But it was their incapability
to perceive their capability to do evil, and the fact that they allowed themselves to be
pushed and pressured one step at a time what turned docile family men and women into cogs
in a monumental genocide machine. And this is true for any propaganda, even the ones that
are spreading about now from the neomarxist postmodernist camp. Because looking from the
other variety of totalitarian regimes, do you think that a bloody society where one third
of the population spies on the other thirds (which is about right for many old communist
establishments) is born because there is a few bad men who just make it that way? Do you
think that the Nazi German came into being because Hitler corrupted the Germans? No, it is
an expression of what the crown felt. Hitler was a smart person, and a great public speaker,
as much as the content of his speeches was absolutely reprehensible, and he knew how to
watch a crowd so that he can tell them what they want to hear, essentially making him a
mouthpiece of the German people in post WWI era. This led to an establishment of a positive
feedback loop, Hitler would say what they wanted to hear, the population would be reinforced
and strengthened in their beliefs, Hitler would gain higher status, would be able to say
other things which were ever so slightly more radical, the crowd would adopt it and be
satisfied, and so on and so on. There is one final realization that we have to come to
kind of introduce into our blood: the Nazis, the fascists and the communists were people
like us. Not some mythical monsters of a seemingly different species, people very much like
us. People, especially fervent humanities students make claims of "how they wouldn't have
bought the propaganda and how they would have fought for the Jews" or "how they would have
fought against communism" (although this sentiment is disappearing since universities are
going dangerously left in recent years, so they do not like to mention communist regimes,
or they claim the "wasn't a real communism/Marxism/socialism" fallacy), but the truth of
the matter is that statistically, this is highly improbable. Most likely, we would have
been all fascists or communists at the times these ideologies were coming to power. Remember
that, and keep it in your mind whenever you are dealing with a pressure of opinion/ideology
from your peers and/or from "above" or from the media. Think, do not just run a script
(to use an IT metaphor), healthily question everything that is presented to you and
exercise critical thinking.

# gjgjgjjgjgjgjgjgu

Lately, I have been thinking about families and parents once again, and their roles,
because there is like a sentiment of not raising girls to be mothers, and less often,
but it is still sometimes expressed about raising boys to be fathers (although any thought
about fathers in the current climate is just fucked, nobody seems to care about them).
And well, to be honest, this should be considered a fallacious proposition from its
inception. I mean, it is of course bad to raise our girl in a way of "try to get married
as soon as possible, have two kids and be a stay at home mom", there should be no debate
about the fact that this is a bad stance to take and a bad view to impose on your children,
but one thing is wrongly bundled with this, and that is teaching "how" to be a great father
and a great mother. And you should teach your children how to be great parents, most notably
by example. And parent gender roles matter, this should be also evident although there are
some deniers, and if it is not self-evident from anything else, just take into mind the fact
that the woman gives birth to children, and she has to care more intensely than anyone else
for the very first period of the child's life. And a proper care has immense, even I would
say surprisingly immense, biological and psychological impact on the child. I read
a study conducted on infants in the US in the 40s, where they tried to deprive babies
of touch and looks, things that mothers give most of during the very first days and weeks
of the children's lives. And what was discovered, and what made this study so infamous,
was that babies who were not touched by their mother figures were much worse off than
the ones who were. Both biologically and psychologically. Half of the babies fucking died.
Most others had severe impacts, and this was just because they were not caressed by their
mother figures. And so, I believe that the topic of proper parenthood and importance of
family is still extremely important and cannot be just tossed to the side easily with
ideological nonsense. Now, let me say something in light of some findings from research
that was conducted by people far wiser than I.

What kind of relationship do you have with your father? It is often ambivalent, right?
Because there is an element of him that encouraged you, hopefully, because without the
encouragement of your father, the world is a dismal place, it is very difficult to be
a courageous person unless you have your father in body and spirit behind you. We know
as much. It is very demoralizing. Well, it really kills people not to have their mother,
they just do not recover from that. And it is possible to recover from a fragmented father
relationship, but it is the next worst thing. Because if your father rejects you, or does
not form a relationship with you, it is as if the spirit of civilization has left you
outside the walls as of little worth, it is very difficult for people to recover from
this predicament. So the father should be an encouraging force, but can
be a tyrannical and crushing force, so that is a very difficult thing to
get right, partly because "if you are my child, then I should impose the
highest standards of behavior on you, and I should always be judging what
you are doing". But I should be judging you with the aim of making the best
in you come forward, but getting that balance exactly right is very difficult.
So it is easy for a father to swing too much into judgement, let's say,
and of course, mothers can play this role too. To swing too far into the
domain of judgement and to be too harsh. And to the degree that the father has
his own pathologies (and everyone does have some pathologies), he is going to
do that imperfectly. He might be someone who is "the father to devours his son"
(and the discovery that this type of fatherhood exists and should be avoided
is known for millennia, just look at the creation myths of some of the popular
mythologies - the world does not develop until the devouring father is gotten
rid of) because he is jealous of the new possibility, the new potential, maybe
also the struggle for attention and love from the mother or from the other children
in the family, there is all sorts of things that can go terribly wrong.
And then, there is the symbol of Father - The Wise King, and that is another
symbol that is being lost to a massive degree in modern world, especially in
universities because all we are taught is to tear that down, and to not even
notice that it manifests itself everywhere.
And well, like I said before, the opposite of this is the Father - The Tyrant Who
Devours His Own Son. That is similar to the mother who is too overprotective, that
is the female version of that. And the mother that is too overprotective is bad also
because she says "I will never let anything happen to you", and well, the thing is,
maybe you actually want to have something to happen to you. It is a somewhat all-inclusive
statement, it should be more like: "No, I am going to make you strong so any
number of things can happen to you and when you need some care, I will be there,
but otherwise out into the world with you". That is the right attitude, and same thing,
we have known this for years. And for father, the correct attitude would be something
to the line of: "Get your damn act together, but I am on your side, it is not
because I want to destroy you or demean you or push you down the dominance/competence
hierarchy, but because I want the best in you to emerge." And so you need standards,
like "what are you doing wasting your life? There is way more than that to you! Get
your act together! And bring it out!". And that is a message that people really want
to hear, if they have any sense at all, and generally they do, and they do want to
hear it.

For a really important chunk of your life, parents (or the people who have the role thereof)
are the most important people in your life. And so it stands that when you are a parent,
you should do your best to ensure your child can stand up to the difficulties of the world!
Not harm them, not abuse them, not shelter them, not demean them, not see them as competition,
but to make them brave and strong, and help them become their own people. And there is this
lesbian anecdote I heard a while back, maybe saw it on Tumblr, about a woman who
was lamenting that their daughter is a lesbian, to which the contrived heroine of the story
answered something like this: "Well, you should be proud. Most parents still just dream of
their children surpassing them." And that is exactly the right attitude! You should do your
best to ensure your children can be the best they possibly can in the world. And if they
surpass you, if they can do things you weren't able to do, you should feel nothing else
than pride and accomplishment! (A whimsical note to stereotypical Asians: just studying to death does
not mean becoming a better person :^) but it applies to everybody, I am just joking.)

# goddddd

This one will be a quick one. It disappoints me that people claim Nietzsche to be a nihilist,
we fundamentally wasn't. He viewed the emergence of nihilism as a kind of cultural pathology.
And everyone keeps mentioning Nietzsche's quote of: "God is dead." Some idiots even scribble
it in random places or use it to motivate their seemingly nihilistic agenda (because most of
those who claim nihilism have absolutely no idea what nothing it entails). But that is not
what Nietzsche said, he said: "God is dead and we have killed him, and we will never find
enough water to wash away the blood", which is pretty much the opposite of a triumphant
proclamation, it is more like a catastrophic loss of meaning. And this seems to be right.
With the contemporary hate towards all sorts of faith and belief (and I must admit that in
my earlier years, I was one of the fervent atheists as well), there does in fact exist a
massive cultural void, a void that begets either nihilism or subscribing to a radical
ideology, lest you have to figure out your own set of moral values, which has proven
difficult for most people, and which Nietzsche believed to be largely impossible on
a cultural scale (see his Ubermensch writings, they are very different from what you
might think if you have heard about this idea from the Nazis, since Nietzsche's malevolent
sister had a tendency to heavily edit his writings in such a way that they would fit and
support Nazi ideology, which would have been without a hint of doubt something Nietzsche
would abhor). And, like Kierkegaard says, for everyone there once comes a midnight hour
where they have to take their mask off, and my question is: will you reveal a giant void,
a black hole where you face should have been? Or will something awful and toxic spill out
of your face the moment you remove your mask? Or... will you be one of the few who manage
to face the horrors of the world and complete an arduous journey through the obscure waters
of morality and ethics, of good and bad, of false meaning and meaninglessness, and come out
as a person who has their own face under this mask, and perhaps does not need to wear one at
all?

# enggglglsl

Curious fact. When I started writing this journal, I wrote it in English
without really knowing why, I just found it easier to think in this language
about complex matters, and maybe I found it easier to express myself, too.
I did not question this for the longest time, but last few days, I have been
thinking about that exactly. Well, turns out that this is actually related to
known psychological effects. And that is that you express yourself differently,
and even act differently in different languages. This effect is most profound
in bilingual people. I do not know if I would really qualify, but English has
been somewhat drilled into me by my family since I was four years old and I
have used it extensively, mostly in writing, ever since. I have, of course, not
been able to speak reasonably good English for the entirety of my tenure, so to
speak, but very early on, I started inadvertently thinking in English too. And
well, turns out that you may be able to reason better in a some languages, and
I think that this is the case. I suppose that another thing, due to my periods
of loneliness and exclusions from the school collective was that there were
many days in my life, where I spoke more English than Czech. Because I spend
the entire days reading English text, my operating system is in English, the
internet I partake in is decisively English, I talk to English-speaking friends,
I read English research, I watch English-speaking series, and I sink fucking hours
upon hours into enjoying all sorts of memes, and so I guess it kind of makes sense,
haha. I know that there are some differences between my Czech and English persona,
or perhaps, it would be better put as "different aspects of my personality manifest
in different magnitudes depending on the language I am currently speaking and thinking in".
I wonder what would it be like if there was a third language that would become my blood
like that, would I develop a third side (and the research suggests that may be plausible),
or is it too late for me to adopt another language so deep into my core? Language, the
meaning of words, a curious thing. I believe that we should value our languages and the
words we speak and protect them. Because the ability to voice your thoughts is holy. Language
needs to be free, and freedom of speech is a must. That is all.

# asdijdaoijds

I have been doing a lot more gardening than usually, these summer holidays. It is a
really nice and relaxing thing to do. I am glad to see that my tree is doing fairly well,
it is somewhat crooked and it will forever be, and its health still may be a little fickle,
but it is now looking proud at me. "I have taken beatings of nature, but I have survived,
now I stand tall face to face with the world, and I will survive and strive for the best."
I like that. I also briefly had mushrooms this summer, I managed to scour the forest
for some Ramaria mushrooms, which are quire surreal looking and very different to what you
might expect a Czech mushroom looks like, and I tried to keep them alive for as long as I
could, and it was actually successful, I think they lived out their above the ground cycle,
so to speak, I hope they show up again when the conditions are once again favorable.

# rrrrrrrrrrrrrr

A lot of strange, stressing and disheartening things has happened to me over the last two or so weeks.
Somehow, all sorts of things have decided to rain down upon me at the same time. There was
this one guy that I knew since we were little children that I would sometimes talk and have
a pretty friendly relationship with, and he died in a tragic manner. It quite hit me and it
reminded me of the dangers we sometimes face. And what rubbed me the wrong way as well was
that the media took the guy and posted photos (albeit a little blurred out) of his corpse
online. And they branded him a suicide. He was not a suicide, it was a tragic accident, but
tell that to the media that made him out to be mentally unstable. And during all of these
things, the one thing that kind of took me by surprise the most was what Minion Girl did.
She and her class were going for a trip to England and it was quite a stressful trip for
her, no doubt, she said it, and during the entirety of the trip, she was acting really weird
for some reason. She was cold, unresponsive, snarky and sometimes even mean to me, and I could
not figure out why. I figured that it was just hard on her and that she isn't feeling well, so
I tried to be mild and supportive, but to no avail. When she returned and kept acting the same
way, I asked what was going on, and she attacked me with a really meanly put question of whether
I am romantically interested in her or not. I answered truthfully that no, that I never thought
of her that way, but that she is really important for me and that I really value her. She was
my only confidant and support after all, one of the few people that were aware that while I am
very durable, I get sad too sometimes. And well, she understood my sincere answer as the exact
opposite, and apparently being romantically interested in her begets punishment, so she was
really not nice to me right when I was the most vulnerable. It's a shame, I miss her.

# iiskjdjdsjdsj

I have been having a strange dream lately. The setting is irrelevant, it is some old building
and there are many other adversaries. I, as magnusi, on a metaphorical level merge with my
feminine counterpart, who isn't a one person, but rather like an abstract idea or a concept,
something intangible yet real, and when I do, I am set on fire. I am set on fire and I grow
large horns, becoming The Devil of All Earth. However, what I do next is that I grab at my
horns as strongly as I could, still all blazing and everything, and I break off my two large
horns, throw one away and stabbed myself with the right one into my left shoulder. And it is
this realization of pain that allows me to take control of the flames and tame them to be under
my control. My eyes stop burning and I can once again see and in some parts of my clothes and
body, there is no longer a burning fire, but cinders, which are not as hot too touch. And every time
I am holding the right horn before I embed it into my shoulder, I think "this is a rib". And I
am really not quite sure about the meaning of this imagery, but perhaps, I think, it may be
that I wish in a biblical sense to be reunited with my rib, wherever or whoever she may be, and
that brings the entirety of my power out, but also limits it to a manageable degree. And this
has been true for many people in my life. So long as I have someone who benefits from what I can
do, I am an unstoppable force of nature, who is capable of doing very hard and perhaps even
tedious long-time-taking things. But I am not sure, but I think I should make a better effort
to understand my dreams some day.

# sadasdaddddddd

We know from research that empathetic understanding, that is understanding with a person,
not about them is such an effective approach that it can bring about major changes in
personality. Sometimes, you may be feeling that you listen well to people and that you
have never seen such results. The chances are very great indeed that your listening has
not been of this empathically understanding type. Alright, and how to listen properly?
Well, we can take the approach that good therapists have. And this one of the techniques
that we can learn from therapists that is exact, not vague like many of their suggestions
(not saying that they would be bad suggestions, far from it, but it is sometimes not easy
to make sense out of a suggestion that is more of the abstract variety). It is like a
little exercise to teach you how to listen to people. So.

The next time you get into an argument with your romantic partner, or your friends or with
a small group of people, stop the discussion for a moment, and for an experiment introduce
this rule (you also don't have to be formal about it):
"Each person can speak up for themselves only after they have first restated the ideas and
feelings of the previous speaker accurately and to that speaker's satisfaction."
Now, this is very cool because here is the typical argument: "So we are arguing and
I want to win and so you tell me a bunch of things, and so then I take those things and
I turn them into the stupidest possible representation of those things. You know, I weaken
your argument and make you look like a fool, and then I destroy it."
And that is a strawman argument, you are making your opponent into a straw man. You take
what they are telling you, you caricature it, in a sense, and that way you can make them
look absurd and make them be ashamed, and then, of course, you have set up this skinny
little opponent that you can just demolish with one punch, so to speak. It is a corrupt
thing to do, and it shows that you are a coward because what it means is that you have to
have an opponent that is crippled and starving and inarticulate before you could possibly
win, before you could possibly progress. It is an absolutely pathetic way of having an
argument. What you should do is listen to the person and help them make their argument
as strong as you possibly can, and then deal with that. Because then you are sure that
you are taking them seriously.

And regarding the "and to that speaker's satisfaction". This is also very cool, so
we are having an argument, maybe it can be about something kind of actually trivial,
for example, who will be doing the grocery shopping in the household, or the dishes and stuff.
Like these little things that continually cause couples to be at each other's throats.
So you will have some arguments about why you should do whatever it is you are going to
do, and in order for the argument to progress, I have to tell you back what you said,
and you have to agree that I put it properly. Well, that is so annoying, right? Like it
just runs very contrary to what you want to do, because of course, you want to make
the other person sound stupid, so you can beat them. This way, you cannot do that,
because you have to listen well enough so you actually understood what they said, and
then you have to formulate their argument so that they are willing to agree that that
actually constitutes their argument. Well, that is really difficult, but it is so useful
because first of all, it does mean that you understood them, and second of all, it immediately
indicates to them that you are not just trying to win (and if you are just trying to win in
an argument, shame on you), you are trying to listen, and then they are much less likely
to get irritable and angry at you because at least you are trying to listen, you are not
making them into a fool. And often when people are trying to tell you what they want, is
that they are afraid of telling you what they want because, maybe, they never got what
they wanted in their whole life, you know, if they had a history of bad relationships,
for example, and poor parenting and so on. They are just damn terrified to tell you that
they might actually want something. And so, as soon as you indicate to them that you have
actually heard what they have said, and you are willing to take it seriously enough to
formulate it properly, well then it is like one step towards to mutual trust. "I see
you did listen, at least you know where I am coming from". That does not mean you agree,
just because you understand someone's argument does not mean you have to agree, but at
least you know what the argument is.

And this extends to more than just arguments. You really need to try and understand what
the other side is all about. And you need to understand in such a way that is compatible
with the person, and people are creatures that fundamentally yearn for understanding, I
think that I am a very clear example of that. My loneliness is because I have trouble
finding people who would listen to and try to understand what I say, nothing else really.
And this is really important for people, you really need to make sure that you know how
to listen to people, and you have to make it visible too, so that they know that you are
actually listening to them and not just "absorbing" their words until their statement is over
and then just saying whatever comes to your mind with little regard for what they said.
Understanding is important, connections are important, and the ability to discuss, to have
a proper argument is important, perhaps especially in these times where the rifts between
people seem to me so large.

# ioasdoijoidsa

So the coronavirus pandemic has finally reached Europe properly. But my man Laurens
has also finally found "The One", it seems. A girlfriend, who is extremely intelligent,
very pretty (although not my type), very well read, very kind and caring and who likes
Laurens very much, and vice versa. I am really happy for the guy. From what I have seen,
and they have both spoken to me because Laurens was so proud of her that he had to introduce
me to her, haha, and I see that this relationship has the predictors to be a successful one
in the longterm. However, to make their love a reality, there had to be a sort of a
"mission impossible". Since Diana, the girlfriend lives in Germany with her kind of
shit parents, and Laurens is in Belgium, they had to get together before the countries
lock down, that is, very quickly. And so they made what was in essence an escape plan.
Where Diana, as a responsible adult nearing 25 years of age, will basically run from
her abusive parents secretly, and board a train to Belgium. However, the trains were
kinda stupid, and she needed to be surreptitious about it, so she would take a train
which goes to Belgium, but not to the correct place exactly, and during the night, of
course. Meanwhile, Laurens would go out into the night in his car and meet her at the
train station, where he would pick her up and then together, they would go to one of
his fathers many properties in Brussels, which he kindly offered to Laurens to live in
with his girlfriend. It was quite stressful, they were worried that Germany or Belgium
might close the borders before they manage to execute their plan, or that Diana's
parents will find out the plan and beat the shit out of her, but in the end it was
successful, and not gonna lie, they now a relationship that many would envy, Laurens
does his best to keep me updated. Once they arrived in Belgium, Diana immediately
started learning Flemish and turns out that she is very good learning languages, and
she got a temporary job as a barista in one of Laurens's father's bars, which is just
for a short while before she finds something better. She also already found a college
she wants to enroll in, to complete her medicine education and fulfill her intention
of becoming a doctor, which she could not before due to her parents. Quite a thrilling
story, really, and they have a really good attitude. Right now, I am just wondering
how many years it will take before the marriage announcement (and hopefully invitation,
haha :^)). Cheers to Laurens and Diana.

# brmbrmbrmbmrmbrm

Lately, I have been curious about dreams. It is because they are this another completely
different mode of thinking that exists within us and that only reveals itself to us during
night. I have already outlined the positions of Freud and Jung on dreams before, and Freud's
method of psychoanalysis of dreams. My dreams are kind of weird, because they vary between
absolutely abstract and surreal and fantastical experiences, and dreams that look very much
like everyday life, sometimes confusing me whether some things have happened or not. My
dreams and daydreams are also connected, and I get a very special kind of dream I quite
can't put my finger it. It is like a non-visual stream of fake experience that are completely
believable. These occur usually very near morning and they are usually about messaging someone.
So despite lack of any visual or audio stimuli, my brain is going through the motions and
reactions of messaging someone, and then I come to my senses and I am often confused about
that as well, sometimes thinking I did actually have that conversation with someone. And
the conversations are extremely believable, like there is some part in my brain that can
very accurately record what a person is right and then extrapolate new material from it. It
is very curious. And so what I am wondering about is what is the biological purpose of dreams,
and frankly, it does not seem like anyone knows, really. Now, my theory is that they are attempts
to make sense of our conditions and experiences, that they are basically thought, and like Jung
said, rather than there being an internal censor, this is the best this type of thinking can
do to convey meaning. And we know two things - the centers for logic and straightforward thinking
are somewhat inhibited during the dream-producing periods of sleep, and there is a chemical
being released that paralyzes us so that we cannot really act out the movements we do in dreams
in real life also. This is the same chemical that is responsible for sleep paralysis. And now,
everyone knows that when they have sleep paralysis, they see and sense all sorts of strange
things, for example the presence of demons, and shadows, and auditory hallucinations sometimes
also. This is because this chemical is a hallucinogen. What if the strange nature of dreams
is due to these two aspects working together? How would a person's dreaming change if you were
to inhibit this chemical and also put him in a safe environment where he would be suspended
or something so that they can move about freely? Would they make more sense? Would they be
be less fantastical and bizarre? Would they be less abstract and metaphorical? I do not know,
but it is an interesting thing to think about, although I do not think that anyone would be willing
to try this experiment, and I am not even sure if there is a way to inhibit this paralyzing
agent. Hmm. Curious.

# uuuuuuuuu

During last two summers or so, I had developed a hobby of taking walks, they
have been a place where some of my most profound thoughts were born, and they
were adventures of discoveries of the unknown, and a way to get myself in the
right state of mind, no matter what else was going on. I share this passion
with Kierkegaard, who put it as such: "Above all, do not lose your desire to
walk. Everyday, I walk myself into a state of well-being & walk away from every
illness. I have walked myself into my best thoughts, and I know of no thought so
burdensome that one cannot walk away from it. But by sitting still, & the more one
sits still, the closer one comes to feeling ill. Thus if one just keeps on walking,
everything will be all right."
But now, the quarantine has begun and I am not allowed to go for walks, I am stuck.
I stagnate, and though I am not as depressed or distressed as others immediately got
and probably will continue to get, I am somewhat lonely. But, I have once again went
into my leg recovery mode, so I do what I have always done. There are also the maturita
exams, so every morning I wake up at a random hour and I start writing my final humanities
thesis. The topic is the distorted image of mental illness in media, something that irked
me for a very long time because almost every time I see some TV show trying portray one
of a specific subsets of illnesses, their portrayal is usually bad and it does no
good to both the general populace and the sufferers of the given disorder. Some disorders
are vilified and so the less informed person might develop a fear of these people,
one that is usually unfounded, since sufferers of mental illness are on average much
less violent and dangerous to others than the general population. Other disorders are
glorified, romanticized even and that leads to having an improper attitude towards the
illness as well. And then, you get a wave of your local snowflake express from mainly
Tumblr and Twitter, but also other social media, who, self-diagnose mental illnesses,
often based on wrong definition and with zero input from a professional, which is also
detrimental to the sufferers of the given mental illnesses, and also the people themselves,
if they in fact suffer from something. Nevertheless, during the pandemic, I think
it will be interesting to observe, how will the society and relationships change.
I suspect there will be both positive and negative effects. I reckon that people
will for example mostly learn that there is a lot of things you can do online no
problem, perhaps with maybe an even greater effectivity. And that even the most fervent
no-I-dont-need-people bravemen will realize that everybody needs someone, and that
social contact is an extremely important aspect of life if you want to maintain a
good mental state and avoid sanity. Curious.

# qwertzuiop

Let me corrupt Kierkegaard's quote: "In addition to my other numerous acquaintances,
I have one more intimate confidant. My loneliness is the most faithful mistress I have
known - no wonder, then, that I return the love." I have not left the flat or seen or
spoken to face to face with anyone but my grandma for some time now. I am not on the
verge of collapse or anything, but I lack social contact more than before. All I get
are messages from people for who feel terribly in the quarantine, which is quite
disheartening. I try to do what I can to cheer them up, but in this climate, it is
of limited success. Hopefully, the situation will improve over time.

# úplounknonl

No one expects the Spanish Inquisition, and no one certainly expects Minecraft Girl
crashing through the roof straight into my life during a time when I most needed someone
to talk to. She just came in like: "Hey I will be returning from the mountains at X date,
you wanna play Minecraft?" And I was like: "Yes, hell yea." And so we did and we have been
doing this everyday after 8pm without fail. And now, I have something to look forward to,
and a person to hear and talk to every day, who is more in line with the things I usually
want to talk about than my grandma or close family members. It is pretty cool, and actually,
if I also add talking to my other friends every now and then, I feel more socially engaged
than I did before the quarantine. It is pretty great, I haven't been this happy in a long
time, I reckon.

# asdksap

Handling ideas, Nietzsche and hypocrites. Nietzsche is often classed with the
existentialists and there's two real tenants of existentialism (well there is
more but we are oversimplifying for this). One is that life is a problem, and
it is not because there is something wrong with you, it is that life is a problem,
and that is often contrasted with the Freudian view which is that "if you have
a problem, it is because something went wrong during your development" The
existentialists said "no, it is like 'life is a problem, make no mistake about it'.
The purpose of scholarship and education is in some sense to solve that problem.
For Nietzsche, he said "all truths are bloody truths to me", and what he meant by
that, was that if an idea didn't incarnate itself in you and transform your
perceptions and your actions, then you were merely possessed by the idea, you
were merely a spokesperson or a mouthpiece for the idea. Or, alternatively, you
could say that the idea possessed you - that you are a puppet of the idea: It is
not you, it is the idea is in you and it has you in its possession. You have not
taken the idea and incorporated with you and made it part of your life, and so
there is a romanticism that is associated with that. That would be the passionate
scholar for whom ideas are not merely abstracted representations that can be tossed
about as if they are commodities, but they are more like personalities (Jung would
definitely agree with this stance), that might be another way of thinking about it.
There is  one thing I learned a kind of a long time ago, I think I mentioned here
as well. When I was lil shit, I liked to argue and I liked to win arguments or lose
them (well I did not really like losing them), although I liked winning them a lot
better. But I did not really care what the content of the argument was, I could
engage in it like a sparring match, just as if I was fighting with the other person,
and it was, in some sense, a battle to establish intellectual dominance. I quit doing
that later on because it seems like it is a crappy approach to the ideas, both mine
and others', since they are not commodities, like I said. That sort they are there,
the ideas. And they have like tendrils or tentacles that reach down into the living
beings, that might be a better way to think about it, Nietzsche's criticism of scholars (and boy, did he enjoy
criticising scholars a lot) was that they were bloodless. Because they were full
of performative contradictions. They would say one thing, and do another, because
their intellect was completely dissociated from their actions and Nietzsche thought
that was a very bad idea, and I think that it is a good criticism. Yes, I think that
it is a bad idea. I also think it makes for an extraordinarily boring lecturer,
especially when I am watching these lectures on Youtube and the dingus who is lecturing looks nothing like
what they preach. You know, because you can tell, if you are listening to someone,
whether the ideas that you are hearing are just being passed through the person as if
they are being memorized say or whether they are a part of the core of the person and,
if they are a part of the core of the person, then they're almost always engaging and
gripping and a million times more interesting to hear and think about. And so Nietzsche
was not a fan of 'bloodless' scholars, and I think that is correct because one of the
things that I see is that it is not a good idea to have ideas possess you unless you
know what the ideas are up to and a lot of people are possessed by ideas rather than
possessing them, and what that means is they have not taken the ideas and integrated
them into their own being. It is like an incarnation in a sense. They have not
incarnated the ideas in embodied form and so they are incomplete, in a sense.

Nietzsche also spoke about Zarathustra, or Zoroaster, an ancient spiritual leader from
Iran who founded Zoroastrianism, which is one of the oldest continously practiced
religions in the world. So, when Zarathustra comes down from the mountain he sees a
bunch of people gathered around a famous individual, it was probably a scholar, but
that really does not matter right now, and when Zarathustra goes and looks at the
person all he sees is a tiny midget with a gigantic ear. So this scholar is like a
hyper-specialist, and so he has a pretty impressive ear, but he is only tiny otherwise.
And that was Nietzsche's metaphorical commentary on the danger of hyper-specialization
and also on the danger of excessive praise for hyper specialization because he thought
about it as a kind of deformity. Which is among the reasons why, despite not many
people knowing this, I am not just focused on computers but I interest myself in
pretty much any field that comes my way.

And so, Nietzsche was a pretty harsh man but he addreseds the issue of the relationship
between intellectual knowledge and action because, for Nietzsche, those things are not
to be separated, so to speak. And well, the definition of the person who does that,
who, in essense, splits what they preach and what they do, is the definition of a
hypocrite. And being a hypocrite is generally not a good idea for your position in
society and your mental well-being in the very long term.

I believe that this also relates to this, in some sense, existentialist belief of mine,
and that is that people believe not what they say primarily, but what they do.

# help me help you

So during the quarantine, I have been pretty much spending my days
gaming with Minecraft girl in the evening and during the day, I
would study all sorts of things, sometimes talk to people and sometimes
game and or waste my time doing other things. Sometimes, this would be
wanking or sleeping. I have spend maybe even over a hundred of hours,
at this point, listening to psychology and philosophy lectures from
different speakers and I have been curious in greater degree than before
about psychotherapy, a field within psychology that has been for me
only secondary, where I would just absorb what I would have randomly
read or listened to without giving it much thought. And now, I have
been more interested in it and I was trying to formulate some overarching
answers to the question of "How do you help someone who is struggling,
especially when they can be considered a 'difficult' person?" and I
heard one clinical psychiatrist / psychologist / psychotherapist speak
about this in regards to Borderline Personality Disorder, which is one
of the most difficult disorders to deal with, and so I would like to kind
of rehash what this person had to say about it, and kinda expand from that.

So the fundamental way one can help a person suffering from BPD is by example.
And that is not like precisely. Let's consider more than just borderline personality
disorder. The question, to some degree is "how do you help someone that's lost?",
and the answer to that is: if they are not willing to not be lost, then you
cannot help them. And this something that can be said and often is from a
clinical perspective (and I know that from my own experiences with people too).
It is a statement that is informed by both knowledge derived from tradition and
mythology and from psychological research and experiences of psychotherapists.
One of the things that Carl Rogers pointed out, who was an American psychologist
particularly focused on humanistic approach to psychology, is that there were
necessary preconditions for entering into a therapeutic relationship. And that
would also be really any relationship where the mutual flourishing of the two
people involved was the paramount goal. One of the preconditions was that
both people had to want that to happen, and Rogers believed he did not know
how to "get the horse to drink once you brought it to the water", so to speak.
And this is one important thing to consider because when people are really lost,
they are sometimes so lost that they cannot be found. And the only thing that
you can do in a situation is get your life together, and manifest the reality
of an alternative mode of being, that's what you have got. And so that is the
only real way for someone to solve an intractable problem like that, and the
reason we are going this direction with regards to Borderline Personality Disorder
is that because it is one of the most serious of the personality disorders, it
is very difficult to treat. And so, we can generalize from that to situations that
are very difficult to deal with, and there is a statement too, and this one has
nothing to do with Borderline Personality Disorder in particular, in the New
Testament that is really vicious, but like many things found in religious mythologies,
it contains a type of wisdom. And it is: Don't cast pearls before swine (we know
this as a general saying in Czech Republic too, not many people know it is from the
New Testament). And what that means is if you are trying to help and it does not work
then stop helping, it is not helping. It may be just wasting your time, it might be
making things worse. Now, if you are offering something and it is not taken,
then perhaps you should be offering it somewhere else, and sometimes, if you
offer hand and the person will not take it, you have to stop offering the hand.
And then what you do is you go off and you have your life. And sometimes that
means in people's life, for example, that they have to leave their family members
behind. There is a scene in the New Testament, this one is also very harsh, where
Christ is walking down the road with his disciples, and his mother calls to him
and says that he is supposed to come back to his home because his uncle has died,
and there is going to be a funeral, and Christ turns to his mother and says something
to the line of: "Let the dead bury their dead, I am doing my father's bidding."
And you read that and you think "well, that should have been edited out", but it
should not have been edited out because it is exactly right. Sometimes, the thing
you have to do is walk away because there is no other solution, and if you are
trapped in pathological relationships and you see no way out of them, if someone
who is sinking has their hands around your neck and is pulling you down, you are
not obligated to drown with them. There is rule too for lifeguards: how do you
approach someone who is drowning and panicking in the water? The answer is like:
I will save you, but that does not mean you get to drown me while I am doing it,
and if it is you drown or both of us drown, it is you drown. And that is wisdom, that
is not cruelty.

And so you need to have the right approach to difficult people: be there for them,
lead by example, get your life together so that their see that there is a better
mode of being in the world, but if they do not want to be helped and just keep on
sinking, do not let them sink with you. And I have seen this happen other times as well,
sometimes you need to leave someone, sometimes maybe even if you did not do anything
bad, you are closely related to a person's problems, maybe their mental state has
a penchant for disliking you in particular for no true reason, and if you walk away,
you open a route for things to change, and especially for things to change for the
better. And then some time later down the line, you can perhaps meet this person
once again, and now, you will be both on equal footing and can converse as old
friends, or as real family members, and not be in a constant battle and powerstruggle
with overarching tones of madness because that was bad for everyone involved.

# luioúpoius

Among many emotions considered negative, Resentment is your friend. If
something makes you feel resentful, do not do it. Well, actually, there
is two sides to resentment, one is that you are whiny and immature and you
do not want to adopt your responsibilities and you are whining about it.
The other is that you are being pushed around and people are attempting to
enslave you. So you want to eliminate the first possibility. You have to
think: "Well, am I just being immature and whiny about this, or is it something
that people are reasonably demanding of me?" And if you think that through,
perhaps talk to some people about it, and you reach the conclusion of "No,
no, this is not reasonable", then the resentment is telling you to act,
because that is what you will otherwise end up being in a few yours, with
a thousand things you are resentful about and then you will be in a painful
state. If someone is going after you to do something, and you feel like
you are not getting proper regard or proper response, or you do not think
it is fair, then, well, have some courage, and get ahold of your anger,
and use it, it does not mean that you are right, but if nothing else, then
it means that you can push the person hard enough so that they have to
engage in a dialogue with you, and these are necessary skills to exist
in a reasonably healthy manner in the world. That is all, thanks.

# grrrbrrškrrrr

There exists a rather special time in my quarantined life right now. It
is the time when I go to take a shower or a bath or anything, just being
alone in the bathroom for an extended period of time. And whenever I am
in there, my mind turns on as if you just poured benzine into it, turned
on the engine and just floored the gas pedal. And so I think about things
in a capacity that is at a unusually deeper level than how I otherwise
commonly conduct myself. And once, I had this really important question
on my mind. And it was "how do you know who are your true friends?" or,
phrased differently, "what constitutes a true friend?". Perhaps it was
because of this quarantine situation that I am concerned with this sort
of things, nevertheless, it is a curious topic to think about on your
way to making sense out of the world and finding an optimal mode of
being. Of course, I read up on this and I am taking into consideration
what I learned from people smarter than me and more erudite on the topic,
that is, philosophers and psychologists, per usual.

So the way it looks to me, this is how you know if someone is your friend.
For starters, you can tell them bad news and they will listen they will
not immediately tell you why you know you are stupid and why that bad thing
happened to you and how something worse happened to them once and you know
derail the whole conversation. You, can actually tell them bad news and they
will listen. So that is a good thing and then there is this weirder-sounding
thing: You can tell them good news and they will help you celebrate. And that
is a really good way of deciding who you should have around you because if
they are not this way, that is, if you have someone around you and something
good happens to you and you are kind of afraid to even admit it because "God,
something good happened to you", so you you come out and you sort of tell
someone half-heartedly that something good happened to you and then they give
you like a 'whack' and then talk about some of the great things that happened
to them three years ago or, even worse, the great thing that happened to someone
that they knew three years ago. And so, if you have a person like that, go away
from that person, they are not helpful to you and they are not helpful to themselves
either. Aand so you want to surround yourself with people who want the best for
the best part of you. And you can hang around with weasels and losers that are
trying to pull you down to justify the fact that they are spiraling downhill as
well and you know the upside of that is you do not have to have any responsibility,
which is incredibly nihilistic and I think that I have already explained why that
is a bad idea. And so you can all whine about how wretched life is, and that may
be a pretty attractive idea for some. But I would say it is also a bad medium- to
long-term solution. Therefore, it is acceptable and desirable to try to surround
yourself with people who are facilitating your development and, well, you might
say "Well, i have got some people around, I know them well, you know, and they are
not doing that well and they do not fit into that category" and well, what is your
point? What are you going to do with them exactly? If they will listen and cooperate
with you and move towards a better future, then great. But if they do not pay any
attention and they keep doing the same damn things over and over and they are not
going anywhere and it is painful, then maybe the proper thing to do is say "You just
have your misery, I will go off and have my life and maybe you will wake up at some
point in the future and think there is a better way of being". Because just putting
up with it is almost... well it is what is commonly known as "enabling" someone.
You put up with that sort of behaviour, you are providing tacit consent for it and
even tacit approval and that is a bad idea, fundamentally. You have, I would say,
both the right and the responsibility to surround yourself with people who are good
for the best part of you.

# aposdasdpok

It has now been a reasonably long time of gaming and talking to Minecraft
Girl, and I have learned a lot about her, and I find her to be a very
curious person, in both meanings of the word. There is something, I
am not sure what would be the proper term for it, there is something
lying down deep in the core of who she is as a human that is very much
like what lies deep down within me. And there is just so many things
about her that intrigue me, or that I find fascinating and/or thought-provoking,
and I really want to say so many things about her, but I do not know where to
start. So I will try to start by a comparison.

A long time ago, I was for a time interested in the Myers-Briggs Type Indicator,
recently, I revisted the topic as a part of my humanities thesis for maturita.
I did the test again and I am still an INFJ and I suspect that I will stay this
type, maybe forever, unless something tragic or otherwise life-changing happens.
And while the indicator is, so to speak, branded by both a commercial and pop
culture element which are detrimental to its function and importance, I still
think that it can provide, on a basic level, a valueable level of insight into
the characteristics of a person.

Now, for Minecraft girl, I am not sure about the "last letter", so I will
get back to it later, but for all intents and purpose, I would identify her
as an INFx.

Just like me, she is definitely introverted. Her social battery is undeniably
smaller and easier to deplete than mine, although the difference is not that
huge, I would say that I am more willing to overexert myself and force through
the social exhaustion, whereas she is more responsible in taking breaks from
social interactions. I probably appear more social and extroverted than her,
on the surface, but she operates better in some settings and groups. However,
based on our discussions, it appears that we largely have the same view on
a variety of social interactions and people, that is, for example, we find
the same things annoying, although she definitely has less patience than me
with annoying people. I have less patience with people I consider harmful
in regards to everything that I have outlined in the previous entries of this
journal.

We are definitely both intuitive, and I think that in a very similar manner.
This is related to an artistic aspect, which exists within both of us. Hers
is, given the fact that she is many times the artist that I am, much more
developped.

As for feeling vs. thinking, it appears that both of us place a great value
in feelings and emotions. I have before outlined how I believe them to be the
underlying motivation for many of the things I do, say, and think about, even
though it could be easy for someone to consider me a thinking type. I think
that the fundamental difference between us in this aspect is that she is better
at expressing feelings, whereas I often have trouble making the things that
exist inside come out in a manner that would communicate it effectively with
the rest of the world. On the other hand, I think that through my years of
effort and learning, I achieved the ability to regulate my feelings, however
strong they are, and boy, do I sometimes feel strongly about stuff, to regulate
them better than she can. This can also be related to trauma she went through,
which is a factor that often has an effect on the ability to regulate emotions.
From what she told me, however, she is making great progress, and I am very
happy to see that. Really, words cannot express the warmth I feel when I see
that she is improving and managing to work through her issues and becoming
her better self. Related to this is also the fact we are both very visual
people, not that we would need to see images necessarily, but that visual
aspect is an important part of our experience, not just in art.

Well, and I am not sure about the final MBTI preference, though, judging vs.
perceiving. In essence people who are judging want things to be neat, orderly,
and established, whereas perceiving preference wants things to be flexible
and spontaneous. I think that both of us are kind of inbetweeners in the aspect,
where I am undoubtedly the more judging one. On one hand, Minecraft girl does
things that are planned and she has systems in some things and she is well
capable of forming and expressing judgements on a variety of topics, events
and so on. On the other hand, she is a very impulsive and spontaneous person
for a lot of things, far more than I am. But I also also value spontaneity
and flexibility, for example, I have already expressed that the type of art
I appreciate the most is spontaneous art, and I think that fleibility is an
important characteristic to have. Not to mention that me and the "Nazi from
Poland" have done a great variety of spontaneous things together for as long
as we have known each other. A curious thing about this is that despite both
of us being somewhat on the fence about this qualifier, we tend to be in
opposition to one another in many scenarios. Oftentimes, when I act
perceiving, she acts judging, and when the situation or topic requires
that I manifest my judging aspect, she will probably be more on the perceiving
side. In essence, this makes a sort of a dyad, two connected elements, and
it makes us complement one another in a variety of situations because our
differences aren't usually so great that we aren't able to reach a consensus.
This is a leitmotif present in many aspects of our inter-personal relationship.

There is one final qualifier which is included on some MBTI sites, and that
is Assertive vs Turbulent traits. This one is a great variable for me, at
some points when I have done the tests, I came out as assertive, other times
as turbulent. I therefore suspect that I am standing on the edge between
these two traits. Minecraft girl, I think, is more on the turbulent side,
but I cannot say for sure because these two traits are not as researched
and as such difficult to study and discuss, I feel.

There is a different approach to categorize a personality, and this one
is more closely tied with language and the way people describe others in
speech, which I find really curious. This is the OCEAN model, more colloquially
known as The Big Five. The Big Five observes five major personality traits,
these are Openness, Conscientiousness, Extraversion, Agreeableness and
Neuriticism. Most of current research, as far as I know, is centered
around this personality taxonomy model. There is one interesting thing
revealed from the surrounding research, and that is that about half of
variation between individuals comes from genetic inheritance and half
from their environment.

Now, openness to experience is essencially intelligence, the correlation
pretty much equals one. Wikipedia describes it roughly as appreciation for
art, curiousity, adventure, unusual ideas, imagination and variety of experience.
Minecraft girl is both very open to experience, and very very intelligent.
Now, her trauma works as a limiting factor or a censor for many of her positive
traits, I feel like it still affects her in a profound way even years later,
but there are glimpses where it appears to me as if the pure unfiltered traits
shine through. And so Minecraft girl does sometimes say ideas that are not that
well developed, or she buys into an aspect of a radical ideology (but it would
be a major, terrible disservice to call her an ideologue, she is definitely not
that, she is very well capable of thinking about and questioning what she is
saying), sometimes she is guilty of accepting a too superficial explanation,
but there are also many times where she says things that are profound,
incredibly deep and thought-inspiring like hell. Like she says something
and it really opens my mind to a new avenue of thought and I am like "wow".
I remember, not so long ago, we had a pretty profound conversation and she
recounted how her therapist often wants her to list reasons why she does not
want to commit suicide. And she told me that the primary reason is curiousity,
that she is curious about what happens next. At first I thought, well, there
are a plenty of better reasons not to commit suicide. But this stuck in my
mind, so I thought about it a little more. And well, now that I think of it,
curiosity is not that bad of a reason. Actually, it is a very good reason. It
is a reason that is personal, that concerns your person only, and so you do not
have to worry about losing if your environment changes drastically. Not to
mention that I too, am endlessly curious, this journal is a testament to that.
So it is an absolutely excellent, brilliant reason, and curiosity is also a
brilliant quality to have, and the fact that she figured it out so effortlessly
like this is just mind-blowing for me. Like "wow, you are really smart". And
this is just one of very many occassions where she surprised me by how smart she
was. She is able to discover meaning and infer things very quickly sometimes,
and she is capable of inventing things that are really great and profound.
It's just wow sometimes. And this is also related to creativity, and she is,
of course, a very creative person, and the things she creates are smart,
profound, and they have meaning and value. And it is true artistic value,
the one that I covet in everything I examine, it is just really great. If
she weren't slowed down by the trauma, the world would have long been in
her palm. Just like me, she is a multi-directional person and she can make
herself useful in many fields and she has many career possibilities. All of
those who stand against her, fear the day when Minecraft girl unlocks her
full range of power and personality, and seizes the day because none of you
twats hold a candle to her unbounded potential.

As for conscientiousness, I am probably the more conscientious one, but she
exhibits the ability to plan and be driven as well. This is related to the
perceiving and judging bit. To a higher degree than men, Minecraft girl is
an agent of chaos - I would say that I am chaotic as well in many things, but
I have, for the most part, managed to extract order out of the chaos, so if
we were to be placed on an alignment chart, she would probably lean more to
Chaotic Good/Neutral and me True Good/Neutral, but I have never really worried
about my alignment, since I do not consider it a scientific descriptor of
personality. But that does not mean that she is incapable of planning and
being conscientious about things, of course not. And through everyday life,
she is doing pretty good, although there are events (usually closely related
to alcohol or perhaps other substances) that just make her throw almost
everything down the drain. Speaking of which, she is a funny and heart-melting
drunk, which people tell me that I am also, so I am really curious about
going drinking with her once I am free from my "golden cage", haha.

Introversion and extraversion has already been examined earlier and I do
not believe there is any need to get back to it, this is pretty much the
same as with MBTI.

Now, agreeabless is a difficult trait. On the surface it seems all positive
and desirable, but upon a closer examination it is a negative predictor for
some things. I used to be somewhat agreeable and I fundamentally still am, but
through my experiences I became more disagreeable than before. Despite her claims,
Minecraft girl is very agreeable, sometimes to the point that I believe it may be
detrimental to her. From the things that she tells me and the bits of her
history that she shared with me, it is evident that it is not hard for people
to push her to do things she does not really want to do, and this is related
to what I spoke about earlier. But once again, to call her completely submissive
or weak-willed would be a great disservice to her because she is neither of
those things.

The final trait of the Big Five is called neuroticism. Neuroticisim is the
tendency to experience negative emotions like anger, anxiety or depression.
This is not to be confused with Freudian neurosis or the quality of being
unable to sit still, not twitch and not be in a constant hurry. I would say
that while I was high in neuroticism earlier, I managed to get my things
together over the year. Experiences of Minecraft girl of course turned up
her neuroticism to eleven, but according to what she is telling me, she has
been making steady improvement over the last few years.

But I suppose that these characteristics are just one facet that one might
talk about. There are several things that make me curious about Minecraft
girl. I suppose that my curiosity is being both sparked and sated by the
fact that right now in the quarantine, there is no other person I would
have a more direct and personal access to (my inability to leave this place
notwithstanding) and because I do not think I have ever met a person who
would be so similar to me and fundamentally aligned with me at the core -
even to the point that I do not even point out to her whenever she does
something quirky and idiosyncratic that I do or used to do because I fear
that she might think that I am making stuff up to get into her favors -
and yet gone through such a different development process and had such
different life experiences that at the superficial level (and she thought
this as well before we went a bit more indepth about it) we look like
completely different people who are very little alike. And I find that
really really curious, just how profound can the effect of environment and
development be that on two people who are fundamentally alike that they
end up looking starkly different.

One thing that I am particularly curious about is her memory. Back when
we did some gaming years ago, I do not recall her having such bad memory.
I mean, it is not like she just forgets everything, but it is to the point
that 'forgetful' can be admitted as a descriptor to her as a person. Now,
it is perfectly reasonable that I just was not paying as much attention to
this sort of stuff back then as I am now, but there is something odd about
the particular way in which she is forgetful that makes me come to a different
conclusion than just biological predisposition. You see, I have noticed a
pattern in the things she forgets. I do not have enough data to make this
a blanket statement that applies in all cases, but it appears to me that
she forgets primarily things related to people and activities related to/
done in company to people. As such, she is pretty good at remembering all
sorts of other informations, which I have definitely noticed, she has an
easy time memorizing things, education really is not an issue for her, she
can prepare for tasks which require her to retain certain pieces of information,
and she definitely has a better numeric memory than me (mine sucks, every
math exam is pain because I just keep forgetting the numbers involved in
the fucken zadání). This begs the question, why does she forget the people
stuff? With the data I have available, I believe that the reason is her
trauma. Her trauma is mostly concerned with people and relationships, and
because, just like me, she has very interlinked thinking where things remind
her of other things, and concrete things are closely mentally associated
with abstract concepts and so on, this encompasses many different aspects
of her life. A great issue, perhaps the principal issue in some sense, for
the sufferers of PTSD is that they have trouble confronting the memory of
their trauma. This is caused by the traumatic events being so traumatic
and so outside the frame of what the person can possibly comprehend that
the events are written into memory in an improper way with the amygdala
grossly overpowering the hippocampus. This error essentially has an effect
of a looping record where the inability to process it causes the events to
come back in the forms of flashbacks accompanied by biological processes of
extreme distress, not disimilar to those that could have been felt during the
event taking place. Now, as a sort of a makeshift defense mechanism (I would
prefer not to say coping because it is not really coping), a number of
patients with PTSD develop memory issues, wherein they forget pretty much
all sorts of things that may be in any way, even in any way unimaginable for
the common mortal, related to the trauma, just so that it does not come back
again. Not to mention the fact that by triggering certain biological processes
which PTSD sufferers know in most severe form as the state they are in
immediately preceding, during and after a flashback (but which may also be
in a much milder form occuring during many normal activities seemingly at
random), the PTSD essentially bullies hippocampus which impacts the recollection
of other unrelated things as well. Therefore, I believe that her forgetfulness
is actually a symptom of PTSD rather than an unrelated fact about her. And
this is great news actually because as her conditions continues to get better
as it is already doing, this negative trait will become more and more a thing
of the past, and I believe that in her future life, she will actually turn
out to be even much more able to retain important information. And I am really
looking forward to that. This girl really deserves to do very good in life
and I am really happy about all both big and small bits of progress she has
made during the last years. It is like: "Well, yeah, you knocked me down,
but now I am coming back up and I will be more powerful than ever and there
is nothing you could possibly do to me to knock me down like that again.
Reckoning is now and I am going to show you all that I am better and more
successful than each and every of you who did me dirty". That is like a poetic
future I would like to see her have.

Another thing that sparked my curiosity is the shadow, from a jungian
perspective. The dark side, so to speak. Well, I think that I have done
my fair deal examining my dark side in the last years and trying to integrate
it as I have spoken about before, and I do not think that she really has come
to terms with hers yet. Mine is best characterized as "what if I used my
'powers' for personal gain? Wouldn't it be nice? And wouldn't it be nice to
just screw over someone whom I dislike?" and so it would fit into the 'evil
mage' archetype, which is sometimes associated with INFJ, funnily enough, so
I guess that's par for course. Minecraft girl, however, has a more profound
and I would say subjective shadow, I believe. I may not be entirely correct
in this, but from the tiny glimpses she has let on, I believe that hers
would be best characterized as a tyrannical vengeful spirit. That means more
like "What if I am the tormentor for once? I wonder how it feels to do to
others what has been done to me. What is it like to have complete power
over someone?". This would make sense, since it would be like a compensating
for suffered trauma, a certain want to reverse the positions.

We briefly discussed the dark side of humans and I of course cited a bit of
the knowledge I discovered and the relevant information Jung says about this,
who, I believe, has spent more time researching this than pretty much anyone
else, but she did this things where she puts a dislike on the message, and goes
pretty much "nope, byebye", which kind of disappointed me a bit. She has done
this several times already, and it is usually on things that are outside her
world view, or her philosophy, so to speak. And I would not really mind if she
disagreed with my opinion, but none of these things were my opinions, they were
research, psychological and sociological facts that stand true and are largely
immutable. I even mentioned it with some of them that "I don't like that it is
like this, but it is like this". I think that this very very occasional act of
rejecting facts is the primary thing that irks me about her. It's not good
and it's not healthy.

There is another curious thing about her (well, there is a plenty, but I am
not trying to write an epic of a thousand pages about one friend only), and
it is that she attracts creeps, weird guys, people who are not at all well-
adjusted, or reek of mental instability. This includes in a large portion a
group of people, usually men, now commonly referred to as simps. Most of these
are acquired through her social media, where is has a reasonably large following.
My question is, taking into account other women with comparable following,
but do not get this unwanted attention to such a degree, why is she so popular
with these people? Well, I believe that this begets a multivariate answer.
First, it is simply because she is a woman, this is the one quality that
all of these share, so we can take that as a baseline. This is not exactly
evidence of sexism, as some would like to put it, but women online garner
this type of attention more than men simply for the reason that it is biologically
rigged the way that men are the pursuers and women are the choosers. This
model allowed us to evolve as fast as we did, apparently, and really is not
a social construct as some would like to put it. We have known this for years.
This does not, however, mean that this attention is not sexist in nature as
well. Second, her style is very alternative and unique. I really like
her style, it looks cool, quirky, and often cute as well. However, alt girls
are often for these people attractive because of a notion that alt girls are
easy, and I am not sure where and why this notion was conceived because it
does not seem immediately obvious to me. Maybe it is related to the "alt
girls have daddy issues stereotype", and well, if you are looking for a woman
that has daddy issues specifically, so you can take advantage, then go jump
off a bridge. Another aspect is that Minecraft girl is actually very pretty.
I do not care much for looks anymore (beyond to the degree a person looks is
an enunciation of their personality), and she would not have been my type
originally, as when I was smol I had a very narrow view where I was pretty much
only into blue-eyed blonde girls, but nowadays, these women are the type I am
most wary of, no disrespect. Minecraft girl has a nice figure, a pretty face,
very fancy and very good quality hair, a nice wholesome smile and a bit of an
air of exotic beauty around her. But the best thing about her look, at least
in my opinion, are her eyes. They are very beautiful, there is depth to them,
they exude intelligence and passion and contain the spark of life that I look
for in every human I come into contact with. It is true, especially in her case,
that eyes are windows into the soul, and the soul they reveal is beautiful,
a little melancholic, and solemn. And yet, they sometimes reveal a hellfire
burning behind them, and the desire to be a little funny devil who does quirky
stuff, and in my opinion, this is a good quality to have in life. However,
sometimes, vulnerability can be seen in her eyes, and those weird men, who are
often predatory in nature, can smell it out and seek to take possession of. All
of these simps, are in fact resentful, miserable and egotistical, and their
perceived and conceited niceness is just a mask to deny from both themselves
and others the knowledge that all of them are wolves in sheeps' clothing.

Anyways, I suppose that is about all about this topic. One thing that I would
like to make clear. There is just so much potential and power lying within her.
Unfortunately, it has been slowed down by her life experiences, but I feel it
coming back to surface, slowly but steadily. And I am really hoping that she
just goes and unlocks everything there is to her, the absolute totality of her
personal capabilities, and does some cool stuff with it.

For a lot of topics, she has a tendency to approach them from the exact
opposite perspective I do, and I find that really cool because when we then
discuss stuff, the conversation ends up being very enlightening, and I learn
things or views that I wasn't privy to before, I hope it is the same way for
her as well.

One thing I must not neglect to mention is that if it was not for her keeping
me company as she does, I would have been noticeably worse off during the
quarantine then I am. I am used to long periods of seclusions more than most
other people, I would wager, but with her, it is much better. In fact, I don't
think I was this socially engaged in years, maybe ever. And so, I think that
overall, I will not remember the quarantine as such a dark and depressing time
as many other people will.

Another thing I forgot is her sense of humor. It is very specific, part edgy,
part dark, part cringy, part non-sensical, but for me, it feels right at home.
I just find most of the stupid little things she says funny, and, god is my
witness, that the shit I usually produce myself is pretty much like that.

She also has a very libertarian approach to sexual topics, which I find really
cool because I am a curious person and like discussing all sorts of stuff. So
thanks to her, I was able to learn a lot that people don't readily discuss
otherwise, which is really cool. We discussed our preferences and, safe for the
fact that there is not a submissive bone in my body, I believe, we pretty much
have the same taste, which is very comforting to know since I don't need to
be worried about being a strange sick fuck. I was also able to answer some
questions for her, and, given her experience, I was kind of suprised that she
didn't know these things about the male condition before, so it was kind of
fun. I have never felt like disgust towards discussions of these topics, and
the relating biological processes (I do not get the notion felt by many men
that periods are absolutely disgusting) and it really nice to be able to talk
to someone who feels the same way and sate my curiosity.

There is one more thing that I forgot to touch upon earlier, and this is pretty
much a defense that some might list as a negative trait of Minecraft girl. I
spoke in length about hypocrisy. What she does sometimes is that she says some
things and presents some values but then does something that is in complete
contradiction to what she has said before. And well, a critic might say: "She
is a hypocrite, she does not enact what she preaches. Or she does not believe
what she says." But I do not actually believe that to be the case. The way it
seems to me is that this is actually an evidence of a noble effort. Despite,
failing sometimes, she is trying and she knows what's good and aims towards
that goal, as much of a struggle as it may be. It is not that she does not
believe what she says, I am certain she does, but that she tries her best to
do what she believes, although she fails on occassion. I know she would almost
definitely try to debate me on this, but she is fundamentally a good and kind
person.

I suppose that for the finale, I would like to present a poetic image of sorts.
We discussed seasons of the year briefly, and just like in many other things,
our artistic orientation in regards to seasons is on the opposite ends of the
spectrum. She told me that she loves summer and the summery aesthethic, and I
told her, in a very light tone, that summers have not been good for me, and
that I mostly concern myself with winter imagery and symbolism. And so I would
like to present this image: she is a summer spirit, and I am a winter sentinel.
She is agile and lively and wears a light unrestrictive outfit, one that is
perhaps colorful in the way some of her fashion is, or perhaps adorned with
bugs. I am slower, calm and methodical, and I am wearing dark thick clothes
with a cape to protect me from the cold. I hope that I can show her a more
beautiful, less depressive winter, and I think we are working on this with
our gaming sessions. I hope she can show me a better summer once maturita
and everything is finally over.

# asdjjvfdjksdk

I suppose that a codified description of magnusi, the primary character of
my dreams, daydreams, fantasy/sci-fi roleplays, the lyrical subject of all
that I have ever attempted to create, is in order. I think that my time with
Minecraft Girl might be an inspiration in this regard as well, since she has
written down her ideas as well. Anyways, here goes.

magnusi is a very old powered being. These beings are often referred to as
'gods', although both he and most of his friends dislike this classification
since it implies a sense of egotism, but it is the most commonly used
classifier. In older ages, gods came in generations, magnusi is a first gen
god with a primary affinity for water (i.e. ocean god) and a secondary affinity
for dark (i.e. gods like Hades, Nyx, Shalim, Nott, Zorya, Tezcatlipoca and so
on). Furthermore, gods have a designation based on their primary approach to
dealing with problems. These are attack gods, defense gods, stealth gods,
sensory/observation gods, scientist gods and others. magnusi is a observation
gods with his abilities centered in particular around his sight.

Within the mythology, mag is the very first and therefore the oldest god in
existence, his coming about being brought forth by the death of the first human
child. This alludes to an old job he had as a psychopomp, where he would ferry
the souls of dead children into the underworld. His oldest 'sibling' is the death
god, who appeared when the first human adult died. This older sibling is often
called Kai but is mostly recognized by the name of Amenotokotachi, which he
acquired in the Japanese pantheon. I put sibling in quotations because the
first generation of gods is weird in that they were born out of a world tree
and are not actually genetical siblings. This has led to an interesting schizma
where the first gods consider some of the other first gods to be like siblings
and other to be romantic interests. mag is notably without a love interest in
the first generation.

The second job that was handed to magnusi much later by the other gods was to
rule over Hell and ensure its continuous operation. This position comes with a
curse since by way of watching over liars, it is required that he who watches
them is not a liar himself. Therefore it is physically impossible for magnusi
to utter any lie. This curse is upheld by the entirety of the divine body which
makes it pretty much certain that there is no chance for magnusi to lie ever at
all. However, he can be deceptive with other things, his body, his actions, obscure
phrasing, his gestures, within jokes and so on. This comes in handy since mag
is a trickster god, and in fact, many of the world mythologies' trickster gods
are just different names for magnusi, for example Sun Wukong for when he wreaked
havoc in the chinese pantheon.

Despite being very old, magnusi is nowhere near the top of the hierarchy, he
set forth some ground rules back in the day, but he does not enjoy in particular
ruling over other gods and people and high politics, or any other types of political
activity at all. This leads to him being considered more of a counselor, but
mostly a comedic relief or a nuisance.

In appearance, magnusi is a bit shorter than me, he has black hair, usually
very short, but sometimes longer, unruly and spiky when wearing his signature
hat, he is very pale, and also skinny, sometimes to the point of looking heavily
malnourished and skeletal, although this varias. His face looks pretty much
like mine, except it is much skinnier and a fair bit narrower and he has large
dark bags under his eyes.

His eyes are the most defining feature. They are notable by having a inward
curved triangular pupil with the corners cut off (well, it is as if the curved
triangle stretched past the iris). The iris was originally blue, and in fact,
magnusi is the person who introduced the fabled blue eye genes into the human
genetic pool, but after an event which involved extreme injuries, pain and
long torture, his eyes were so bloodshot that the blood managed to flow into
the iris and dye it red. As a memento of this trauma he survived, a sign of
a change in mentality and also as a psychological weapon, he kept the red color
and actually made his irises be red.

Mechanically, the eyes are special in that they are threaded (like screws) and
how far on the thread the back part of the iris is denotes the distance the eyes
are focused on. Therefore to refocus, both the iris and the pupil must spin. mag
can focus on two things independently, so the eyes can spin independently also.
Usually, the spin is imperceptible to the human eye, but mag sometimes slows it
down as a psychological weapon, that is, to freak out whoever looks at him.

The eyes are called "analytical eyes" and they have much better visual capabilities
than human eyes. They can observe virtually all light, measure distances, look
into objects (by selecting different types of radiation), see sound waves, calculate
trajectories, they have a much wider field of view and differently shaped also
(they can see better to the sides and up because of their shapes), they can
see very fast objects, they have a very high range and also can see very fine
details at shorter ranges, they can calculate how long will certain movements
take, see in pretty much complete dark (this is fixed by the eyes shining),
and pretty much anything else that can be expected from a perfect sensory organ.

After previous experiences, the eyes are also made to withstand pretty much any
damage without it having any noticeable effect on them. They also have a second
stage, where the right eye becomes a circle where one can't differentiate the
pupil from the iris, both kind of melting together and taking on a dark red color,
and the left eye becoming larger, taking on a circular pupil that is concentrical
with two circles. This creates a pupil surrounded by two stripes. Within each
stripe, 'squares' of black and red iris matter alternate. Both stripes have the
same amount of blocks, so that two of the same color do not line up. These two
stripes can spin independently of one another. In this form, the eyes are
referred to as the Time (right) and Space (left) eyes, where the Time eye has
very poor actual eyesight, to the point that it would require prescription glasses,
but can look a very short amount of time into future and a much larger period
of time into the past. It also makes locally speeding up and slowing down time
easier and more effortless. The space eye becomes much sharper and provides much
greater visual prowess and allows extremely fast localized teleportation of
even large objects, bending of space and other related abilities. It is a rare
occurence for mag to use both of these eyes at once, since it is extremely
energy consuming and causes heavy bleeding from the eye sockets, so usually,
mag needs to make a trade-off and keep one of the eyes shut and disabled.

magnusi also utilizes a lot of tiny generally-invisible eye-balls, some of which
he leaves suspended in places that require monitoring, some of which he sends
to travel and observe things around the world, and some of which he keeps around
himself to give him an visual edge in situations. Usually, he keeps at least
fourty of these eyes floating around in his vicinity. This is for two reasons,
heads up, and theatricity (so that he gets cinematic shots for his memories).

magnusi is actually to a large degree theatrical. He telegraphs his attacks,
he makes strange gestures and says some arcane sounding one-liners, intorduces
weaknesses to his strategy, lets himself get injured by his opponents and usually
tries to make fights long and balanced. Most of the things he does in battle are
also intended to scare or intimidate his opponents, and in best case prevent
the battle at all. magnusi does not like needless conflict, and so he employs
ploys and psychological warfare to prevent most conflict.

As for a general listing of powers, it is this:

- hydrokinesis (the primary real power, very many others are derived from this through years of study)
- time dilation
- teleportation (through portals only, the effect of personal teleportation is achieved by opening a
  magnusi-sized portal and throwing the portal across himself),
- supernatural physical abilities
- visual prowess,
- fake telekinesis (magnusi actually wraps items in a nearly invisible film of water, or
  grabs items by their water content),
- swordsmanship
- physical flexibility
- electrical discharge (since magnusi is basically water, he was able to construct a makeshift battery
  in him which electrical attacks of others charge and he can discharge)
- shapeshifting,
- fake intangibility (by shapeshifting into a gaseous form)
- temperature manipulation
- fake levitation (either repelling himself from underground bodies of water or walking on thin films
  of water he can suspend in air),
- space bending (to make objects seem smaller or bigger or to redirect objects, and look around the corner)
- fake illusions (actually mist constructs or tangible constructs which are made to seem to the person like
  they are hallucinating, sometimes, mag can also manipulate the small amount of water that is on the surface of
  the eyes to affect the light passing in)
- very limited form of telepathy (can talk with people telepathically but not read their minds or do mind control)
- extreme regenerative powers (so long as there is energy, magnusi can generally reconstitute, however, due to
  adrenalin circuits being taken out, not only does he feel the pain of every injury the
  same way as humans, he feels it even to a greater degree because there is no adrenalin
  response),
- creation of water clones (they look real but when injured they bleed water and
  when they are destroyed they disperse into water)
- profound knowledge of all Earthly sciences, which he uses to do experiments, study further and sometimes make abominations
  against God in form of creepy monsters (but most creations are not that horrific),
  knowledge of technology which he uses to create all sorts of gadgets,
- survival instincts,
- very poor luck
- cancer blood (his blood is a toxic cleansing agent which heals injuries but also spreads his personality traits
  to those who consume it - that's the toxic part)
- cunning and scheming
- interdimensional travel and the creation and maintenance of pocket dimensions
- light suggestion (basically a devil power, by making an eye contact with someone to spread his eyes - the 'infected'
  look like they have mag's eyes to everyone except other infected, infection spreads through eye contact. The infected
  have a lot of their filters removed, are more prone to be honest and act on instinct and can be lightly pushed to do
  something they want to do at least a bit - so it is a power of light suggestion)
- intimidation and fear inducing
And this should be roughly it, although the power set is really expansive, is not tightly defined
