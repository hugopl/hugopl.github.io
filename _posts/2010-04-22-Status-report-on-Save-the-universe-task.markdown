---
layout: post
title:  "Status report on \"Save the universe\" task"
categories: build_tool c++ development meique
---
I'm talking about my pet project called meique, yes, this is yet another build tool.

The project is going a "bit" slow, I can summarize this situation in numbers, the project had 15 commits so far, 4 in 08/2009, 4 in 12/2009 and 7 in 04/2010. In other words, 4 commits, 4 months doing nothing, 4 commits, 4 months doing nothing, 7 commits, ...

As you can see there is a pattern in meique development, every commit represents 1 month doing nothing! But this isn't my fault, ok.. is my fault, anyway I want to break this pattern, no... no... I'm going to break this pattern!! at least I hope so.

Besides all development slow down I achieved some goals with those 15 commits:

<ul>
<li>The basic architecture to provide the basic functionality is done, or almost done :-).</li>
<li>Meique can now compile basic hello worlds \o/.</li>
</ul>

<h2>So what's missing and what's next?</h2>

Missing? A lot of things. My current implementation plan is:

<ul>
<li>Implement the source directory structure replication, used to the separated build dir compilation feature.</li>
<li>Create a very basic preprocessor, just to identify the dependencies of a C++ file on each run.</li>
<li>Use md5 or a faster hash algorithm to identify when a file needs to be recompiled.</li>
<li>Support multiple jobs, -jN option.</li>
<li>Redo this list with four more items.</li>
</ul>

For anyone interested on meique, take a look at gitrotious <a href="http://gitorious.org/meique">project page</a>.
