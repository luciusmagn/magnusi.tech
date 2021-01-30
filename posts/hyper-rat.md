created = "2020-10-12T11:30:22+01:00"
tags = ["magnusi", "rust", "ssg"]
title = "[EN/IT] Introducing hyper-rat: the most barebones SSG"

Hello, recently, a friend of mine has asked me to develop an art portfolio
website for her. Since she knows `git` and Markdown, I figured that a static web
might be a fun way to do it, and so we did exactly that.

Given the specificity of the art portfolio, using `morpho` didn't seem like a good
option, and so I instead elected to make yet another static site generator.

Introducing hyper-rat: the most barebones static site generator that's still
functional. Sitting at 7 top-level dependencies and 165 lines of generously
formatted code, hyper-rat takes a rather "duck-typed" approach to generating
websites.

1. Static data is copied to the build folder.
0. A hashmap of [Ramhorns](https://github.com/maciejhirsz/ramhorns) template is built
0. Content tags with the format of `[[content_path template_path]]` are read from all
files. This determines what template is used to process each template file. `content-path`
can be a folder in which files are processed alphabetically, allowing you to sort them
and create a sort of posts/articles hierarchy.
0. Content files are read and their headers are processed. Headers consist of abitrary
information that will be passed to the given template. A content-file does not have to
have a header at all.
0. Content files stripped of their headers are processed through appropriate templates
and the content of their headers is passed as context to the templating engine.
0. The templates are rendered to the build folder.
0. Profit??

The source code is here: <https://github.com/luciusmagn/hyper-rat/>
