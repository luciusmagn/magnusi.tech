created = "2021-01-20T19:01:21+01:00"
tags = ["magnusi", "rust", "studying"]
title = "[EN->CZ/IT] Finally about to launch GJK.cat!"

Last year before March, I developped a system for organizing study
materials in a way that resembled a wiki, but with git, Markdown,
as a static website with automatic deployment, and with all the nice
features of `mdBook`.

I ended up achieving this by writing a `mdBook` preprocessor called
`cat-prep` which overtakes several processes and constructs a hierarchy
of subjects, tags/categories, teachers/authors and materials.

I also got a quite nice cat picture drawn by my friend RedPanda. Here
are some links if you want to check it out:

- <https://gjk.cat> - main website
- <https://it.gjk.cat> - instance for the IT field
- <https://github.com/gjk-cat/cat-prep> - the preprocessor
- <https://github.com/luciusmagn/it.gjk.cat> - source code for the IT instance
- <https://github.com/luciusmagn/gjk.cat> - source code for the main website

The automatic deployment was done through ZEIT (now called Vercel). Despite them
not having official support for `mdBook` or Rust, getting it up and running was quite
easy, see the `build` file in the IT repository.

Cheers,
