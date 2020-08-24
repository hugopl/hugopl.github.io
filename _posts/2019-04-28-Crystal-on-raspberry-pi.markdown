
For the ones that don't know, [Crystal](https://crystal-lang.org/) was a 2018 hype (however the project exists since 2012) that I only found in 2019, basically it is a language very similar to Ruby in syntax, but that compiles to machine code and is statically type checked.

I was about to start a pet project using Raspberry Pi and Ruby when I noticed the existence of Crystal, so I used the occasion to learn Crystal, just one problem: There's no crystal in archlinux for raspberry, or at least my efforts to find one weren't enough.

Not a problem, let's compile the Crystal compiler into raspberry! This would be amazing, but Crystal compiler is written in Crystal itself, so we have the [egg-chicken](https://en.wikipedia.org/wiki/Chicken_or_the_egg) problem here, the answer? cross compiling!

## Cross compiling

By my experience with C and C++, cross compile is a hell, but since Crystal is built on top of LLVM, I gave a try hopping for the best... and was very easy! :-)

My tests were using ArchLinux into a rPi, but this is so simple that must work on every distro.

First do a hello world in Crystal, save it as `hello.cr`:

{% highlight ruby %}
puts "Hello Crystal ARM world!"
{% endhighlight %}

Install crystal on your computer, `sudo pacman -S crystal`, then cross compile your hello-world program.

{% highlight bash %}
$ crystal build --cross-compile --target=armv6l-unknown-linux-gnueabihf hello.cr
{% endhighlight %}

To know why the string "armv6l-unknown-linux-gnueabihf", go to the rPi, install the llvm-package and type `llvm-config --host-target`, this is how LLVM describe the platform it is compiling for.

This will compile the file, generate a object file and print lines of code that you need to run in the host machine (the rPi) to link your program, i.e. a GCC command line.

So.... copy the `hello.o` file to the rPi, then we are going to try to link it. But not so fast, Crystal programs have some dependencies, all but one are solved by installing packages, so in your rPi install the following packages:

{% highlight bash %}
$ pacman libevent gc
{% endhighlight %}

The missing dependency is `libcrystal.a`, a tiny one-file plain C static library that we are going to build from Crystal sources.

## Building libcrystal.a

As I said, this library is just a single plain C file, so we just need to compile it and generate the static library **in the rPi**.

{% highlight bash %}
$ wget https://raw.githubusercontent.com/crystal-lang/crystal/master/src/ext/sigfault.c
$ cc -c -o sigfault.o sigfault.c
$ ar -rcs libcrystal.a sigfault.o
{% endhighlight %}

Then you can put libcrystal.a in `/usr/lib/crystal/ext/` or in the same directory of the hello world. The crystal/ext directory is better, since the link commands the Crystal compiler tell us use this, so we need to change nothing.

## Finally linking!

Now with everything ready, just link your object file with the commands supplied by the crystal cross compilation.

{% highlight bash %}
$ cc 'hello.o' -o 'hello'  -rdynamic  -lpcre -lgc -lpthread /usr/lib/crystal/ext/libcrystal.a \
-levent -lrt -ldl -L/usr/lib -L/usr/local/lib
{% endhighlight %}

If you think this is too much job... or you are too young in the cross compilation world or I'm too old to remember how painful was to cross compile anything to ARM.

