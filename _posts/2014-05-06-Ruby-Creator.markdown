---
layout: post
title:  "Ruby on QtCreator"
tags: Ruby QtCreator meique
---

After some days recovering from a [septoplasty](http://en.wikipedia.org/wiki/Septoplasty) I got some time to put love on my new pet, not a dog, not a cat, just something non-organic, i.e. yet another pet project. This time it's a plugin to add [Ruby language](http://www.ruby-lang.org) support on [QtCreator](http://qt-project.org/wiki/Category:Tools::QtCreator), a C++/Qml IDE.

## Why?

Because I want to would be enough, but as I'm in a good mood let me explain in a single paragraph:

I use QtCreator for C++, It's faster and code navigation, auto-completion and refactoring works as expected. I want to have these features when doing Ruby programming, besides it's fun to write this kind of stuff.

So the project is hosted on [github](https://github.com/hugopl/RubyCreator), I'm working on it when I can, however it already have some features:

## Project Manager

QtCreator is a project oriented IDE, however I dislike the bureaucracy related to project setups on most IDEs, so I went to the simpler approach: open a .rb file and all .rb files under the directory will be added to the project, later I plan to add the many extensions used on Ruby and Ruby related files like .rhtml, .ru, etc.

![Project Manager](/postimages/20140506_projectmanager.png)

A project manager means you can type "Ctrl+K" on QtCreator to open any project files.

## Basic syntax highlight

It's working, just need to be improved a bit to recognize regexes, in string variables, symbols, etc. It's very easy to add this, but as the basic stuff is working I'll concentrate on other things and improve the highlight as I need it.

![Syntax highlight](/postimages/20140506_syntaxhighlight.png)

## Basic code navigation

Basic code navigation is working too via the "Ctrl+K menu", you can see (and navigate) all methods of the current file (". " shortcut) or all project methods ("m " shortcut).

![Syntax highlight](/postimages/20140506_ilocator.png)

The backend for this is based on regular expressions, my first attempt was using a Ruby-based Ruby parser but it was too slow for the task taking 6 seconds to parse a 20K lines files while my simple C++ version took 385 miliseconds, still slow but is enough for now.

## Indentation

This is simple, type: "def foobar", hit enter and see the cursor when you expect it to be.

## The future

The features I want to write ASAP are:

* <s>Type "def foobar", "if foobar", etc, hit enter and the "end" keyword is written for you.</s> (done!)
* Variable use highlight: leave the cursor on a local variable and all local variables in the scope are highlighted.
* <s>Basic auto-completion, for attributes is easy, but for method invocations some times is impossible due to the nature of the Ruby language.</s> (done!)
* <s>Code navigation via F2: hit F2 when the cursor is on a method and go to the method. As sometimes is impossible to know the instance type, a small combo would appear like happens when this feature is triggered on a virtual method in C++.</s> (done!)

## How to install and test?

Hmmm, there's no docs at all, so consider the next lines as a documentation:

* Clone the QtCreator sources and go to the tag v3.1.0.
* Compile and install my [beloved build system](http://meique.org/), there's a [AUR](https://aur.archlinux.org/packages/meique-git/) package for it.
* Clone the plugin on [github](https://github.com/hugopl/RubyCreator).
* On the plugin directory, type:
{% highlight bash %}
mkdir build
cd build
meique --QtCreatorSources=PATH_TO_QTCREATOR_SOURCE ..
{% endhighlight %}

* I didn't write a install procedure, so you need to manually copy the files on QtCreator plugins directory, the files are: `libRubySupport.so` and `RubySupport.pluginspec` located under the build directory. On my system the plugins directory is `/usr/lib/qtcreator/plugins/`.

## Conclusion

This is it, if you want to help me on this just mail me, leave a comment or ping me on IRC.
