---
layout: post
title:  "Meique released"
tags: build_tool c++ development meique
---
By a release I mean, I tagged the git repository with some version number (0.8), so you still need to download the sources from git if you want to test it. I wont spend my free time to create a website nor distro packages very soon, because I think that for while is better to spend my time coding than creating cosmetic things for a tool not production ready yet.

Ah, I almost forgot to say, meique is a pet project of mine, result of my will to have a more than reasonable building tool for C and C++, a really good one. I'm doing it on my free time and hope to finish it some day, hehe.

Ok, back to the main subject, it's not production ready... by production ready I mean, if you want to use meique in a near future the best thing to do is to try to port your project to meique and report any bugs and wishes, so bugs can be fixed and wishes turned into reality.

<h2>So, what meique can do until now?</h2>

<ul>
<li>Out of source builds.</li>
<li>Find installed packages using pkg-config as backend.</li>
<li>Support projects with multiple source directories.</li>
<li>Decide if a file need to be recompiled by their contents, not by their timestamp.</li>
<li>Multiple jobs at once.</li>
<li>Detect the file dependencies and also use this information the decide if a file needs to be recompiled.</li>
<li>Automatic creation of the following targets: all and clean (install and uninstall not done yet).</li>
<li>Scopes for OS, compiler and build types, like the ones used in qmake.</li>
</ul>

<h2>What it can't do yet?</h2>

<ul>
<li>Probably there are some (maybe many?) bugs, because I did only few tests and I'm still to lazy to convert my manual tests into automatic tests.</li>
<li>There's no equivalent helper function to cmake configure_file function.</li>
<li>There's no windows port yet, to create it is a matter of create an os_windows.cpp which implements the OS interface, i.e. few</li>
functions inside a namespace (rm, mkdir, cd, pwd, etc).</li>
<li>There's no install function yet, I need to think a good API for it to support Mac OSX frameworks, simple UNIX installs and the mess found in Windows systems, so I wont implement anything until I have a clear and simple API for it in my mind.</li>
<li>Support for tests, something like the add_test function of cmake.</li>
<li>Documentation! Currently the only documentation is the source code itself, mainly meiquescript.cpp and the meique.lua files used to compile meique itself.</li>
</ul>

<h2>How to get it and report bugs/wishes?</h2>

You can get the sources on gitorious (<a href="http://gitorious.org/meique">http://gitorious.org/meique</a>). Compilation can be done  using cmake or meique itself.

To report bugs and wishes write to hugo.pl at gmail.com.
