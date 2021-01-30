created = "2020-04-10T15:32:54+01:00"
tags = [""]
title = "[EN/IT] Transitioning to a static web and the beauty of SSGs"

I have been running my website for about five years at this point, and it
used to mostly host random things, bits of text, C language snippets and
media files.

For the first few years, it ran on my RPI ver. 2 that's been plugged into the
wall in my bedroom and communicated with the network through a usb wifi dongle.
The Raspberry PI is a technological wonder and I had a great experience using it
as a tiny server with Archlinux ARM.

My website was a small server written Rust with the Pencil Framework, which was
on the rise at the time, but unfortunately died a few years later. While the
framework delivered good enough performance, I still had to tackle several
issues.

The first of these was slow internet speed - back then, our household theoretically
had 5Mbps upload on a _good day_, most of the times, it was just unbearably slow. I
solved this issue by having appropriately sized media files and having a minimalistic
design.

The website then had another problem - it was dog slow, unbearably. A request would
take up to 20-30 seconds to be processed. But I just said that the performance delivered
by the framework was good enough, wasn't it? Well, the problem lied in my Markdown
setup. The website generated content from Markdown, but the process was extremely slow.

At the time, I figured that I just gotta do, what I gotta do, the Raspberry PI is not
that powerful, I guess this is the price. However, it wasn't that fast local either.
I fixed this issue by implementing an in-memory cache. For each request, I'd just check
the modified date of the given file against the cache and only regenerate the file if
it changed. I would also pre-generate each of the websites when the server started.

This improved the performance dramatically, but it was extra code and I wanted to keep
it to a minimum. Eventually, I found out that the problem was not really performance,
but that the Markdown library I was using was written horribly and it was that what
had terrible performance. Once I switched to `comrak`, I was able to delete the cache
and still had really good performance.

Recently, through a friend, I have discovered that static site generators are pretty
cool, and so I thought that maybe, I want to try that out for myself. I checkout the
major ones written in Rust, for example Zola, and while Zola is really nice, I thought
it was too large and feature-packed for my minimalistic and hacking-culture-ish
purposes.

I wanted to make my own static site generator, but not really out of scratch. I went
through all the different smaller and sometimes even abandoned SSG projects, and
eventually ended settling with `mdblog`. However, there were still features I
didn't like, features that I found missing and things I would change.

And so I did exactly that, I changed the theme to be more minimalistic, as you can
see, deleted a whole bunch of code, removed several dependencies, rewrote it to use
TOML all across the board instead of mixing up TOML and YAML and also changed the
templating engine to a smaller one.

I have named the project `morpho` and I am pretty content with how this venture turned
out. Of course, I will be adding/removing things as I go, but this looks like my solution
for the time being.

The generated website is quite nice and performant and I am happy with the looks. I
suppose it will take a bit for me to transfer and update all my content, but I have
gotten new enthusiasm to do so.

PS: The website also used to host package information from `pebble`, a package
manager I was developing for the [C2 language](c2lang.org). Since the package
manager is no longer in development, I see no reason to port this functionality
over for now.

Cheers,
