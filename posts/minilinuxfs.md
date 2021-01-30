created = "2017-12-30T13:02:38+01:00"
tags = ["magnusi", "rust", "linux", "git"]
title = "[EN->CZ/IT] Introducing minilinuxfs - a small and suckless linux fs generator"

A few weeks ago, a friend of mine asked me to develop a linux filesystem generator
for him to be used in a chroot jail. The requirements were:

- as small as possible
- as secure as possible
- have bash for running student scripts

I embarked on a journey to create the smallest possible environment, then. I started
by selecting alternative, yet POSIX-compliant, implementations of the coreutils. I
selected the suite developed by the suckless group, namely `sbase`, `ubase` and
`9base` (mainly for awk).

I figured that the system will be most secure if no folders will be mounted from the
host system. BASH does not require any devices to function, so that was a win from the
getgo. The bigger problem were libraries - by default many things link to many libraries.

The solution is quite simple, just compile all of the programs statically. This is often
easier said than done, but, in this case, it was possible to create a statically-built
config for everything, and `ldd` showed no libraries for any of the programs. I used
`musl` libc for all of these, which already reduces the size significantly, due to
being a much smaller standard libary implementation.

Now it's time to reduce the size. There is several things we can do while compiling.
First, we compile for file-size (`-Os`). This already has a significant effect on the
size of the produced binaries. Next, we enable dead code elimination with the
`-ffunction-sections -fdata-sections` flags.

For linking, we enable LTO (link-time optimization) with `--gc-sections`. This further
reduces the binary size, but we can go further. After compilation, we strip unnecessary
information from the binary with the `strip` program.

This is as far as we can go without installing 3rd party software. The final step I have
taken is using the [UPX program](https://upx.github.io/), which is an executable packer
and compresses the contents of the binaries. By using it with `--ultra-brute` option,
I was able to fit BASH and a reasonable userland - while statically linked - into
4 megabytes of space.

The results were quite unbelievable for me.

Here is a link to the repository. Warning: it's all in Czech.

<https://github.com/luciusmagn/minilinuxfs>
