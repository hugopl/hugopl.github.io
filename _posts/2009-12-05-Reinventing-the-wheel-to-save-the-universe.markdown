---
layout: post
title:  "Reinventing the wheel to save the universe!"
categories: build_tool c++ development lua meique
---
I admit myself, I have a bit of the "Not written by me" syndrome, but I guess that this time this is not a side effect of this developer disease, it's just because every build tool in this planet sux in a way or another, so I decided to write my own build tool, yes... the build tool of my dreams!

Before start to talk about it, I like to answer why not X? why not Y? Ok, let's do it one by one.

<h2>Why not Autotools?</h2>

Go fuck yourself.... and GET OUT OF HERE!!!!

<h2>Why not qMake?</h2>

qMake is useful only for Qt-based projects, and IMHO, for the simple ones. Ok, Qt is a huge project and uses qMake, but did you ever found someone spreading good words about qMake? In other words, I never use qMake for my Qt projects, I use cmake instead.

<h2>Why not SCons?</h2>

SCons is somehow a good build tool, last time I used it was two years ago, I like the SCons bootstrap methodology but I dislike the python dependence, summarizing, IMHO CMake is better.

<h2>Why not CMake?</h2>

CMake is the best build tool nowadays, simple use cases remains simple and complex use cases are possible. I use it for all my projects, so I know that it's not perfect yet.

<ul>
<li>CMake syntax is horrible and too verbose.</li>
<li>CMake uses a declarative approach to describe the build process, despite of the declarative nature of the action of describe a project, many times when writing a custom target with CMake you think yourself "If I could use an imperative language, my life would be easier".</li>
<li>CMake is big! 12MB is big!!</li>
<li>You need  cmake installed to compile a CMake project.</li>
</ul>

<h2>Why not X?</h2>

I don't know X, so X is too new or probably not so good :-), but if X is really good, just assume that what I'm doing is a side effect of the "Not written by me" syndrome.


<h2>Why not Meique?</h2>

Yes! Meique is perfect! Is the build tool of my dreams! the holy grail!! but it does not exists yet, the current source code still not useful, I'll push something to gitorious when it be able to compile the first Hello World.

Ok, so let's talk about my vapor ware, first the desired features.

<ul>
<li>Out of source builds.</li>
<li>Self-contained, small, no dependencies besides C++ standard library.</li>
<li>Flexible, extensible and intuitive, uses Lua as scripting language, <strong>an imperative language!!</strong></li>
<li>You can bootstrap it! So you don't need it installed on your system to compile a project based on Meique.</li>
<li>Integrated testing support (like ctest).</li>
</ul>

Meique isn't a meta-buildsystem like CMake, i.e. it doesn't generate files for native building tools like Makefiles, Visual Studio projects, etc. Meique itself call the compiler, take care of what should and what shouldn't be compiled, etc. This adds a bit more complexity to the project, but open the road for useful features like:

<ul>
<li>Decides if a file needs to be compiled by their contents change, not just timestamp.</li>
<li>A single behavior on all platforms.</li>
<li>Update the file dependence list on-the-fly.</li>
<li>I don't need to write a lot of back-ends for a lot of systems that I never used.</li>
</ul>

The Meique Lua API is almost done, I just need to think easier ways to write the equivalent of CMake FindPackages, a simple Hello World could be described as:

{% highlight lua %}
target = Executable:new("hello")
target:addFiles("hello.cpp")
{% endhighlight %}

The stupid example above shows nothing, because build tools intent to be used mainly by medium/big and sometime complex projects, so I'm trying to create a good API based on my experience with CMake, qMake and SCons and why not, my personal hate against Autotools.

P.S.: If you search about Meique, probably you will find an old <a href="http://meique.luaforge.net/">website at luaforge</a>, this was my first attempt to create a build tool, the source code reflects my understanding of building tools 5 years ago, so forget about it.
