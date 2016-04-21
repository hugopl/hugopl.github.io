---
layout: post
title:  "Compiling RubyCreator on Windows"
tags: ruby rubycreator qt
---

I finally spent some time to try to compile RubyCreator on Windows, I don't use Windows and dislike it as a development environment so this is why it took so long, here I'll describe the steps to get it compiled and working, in a near future I plan to do binary distributions for RubyCreator, so will be easy for Ruby Windows developers to get it.

While there is no binary distribution, you need to compile it yourself, so here is the slow and painful instructions, ok, not so painful, but requires a log of time and downloads.

## Overview

To get it done you will need.

1. Patience, 1Kg is enough.
2. Download Microsoft Visual Studio Express 2013 (QtCreator binary distribution was compiled with it, so the plugins should use the same compiler).
3. Download Qt for Visual Studio 2013 (The huge package with 840Mb)
4. Get the QtCreator sources from somewhere or clone it from git (git@github.com:qtproject/qt-creator.git). Try to do a shallow clone to avoid download the whole QtCreator git history.
5. Compile QtCreator
6. Clone RubyCreator
7. Compile RubyCreator

## Compiling QtCreator

As the QtCreator binary distribution does not come with all the data we need to be able to compile any plugin, you will need to compile QtCreator first.

1. Open the MSVC2013 Developer Command Prompt.
2. Add the Qt bin directory to the system path, so you can call `qmake`.
   <pre>C:\> SET PATH=%PATH%;C:\Qt\Qt5.6.0\5.6\msvc2013\bin</pre>
3. Go to the directory you cloned QtCreator.
4. Checkout to the tag matching the version of QtCreator you want to compile, in this case same version of QtCreator you already have installed on your system.
5. Prepare to do a _out of source build_:
   <pre>C:\...\QtCreator> cd ..
C:\...\> mkdir QtCreatorBuild
C:\...\> cd QtCreatorBuild
C:\...\QtCreatorBuild> qmake ..\QtCreator\qtcreator.pro
C:\...\QtCreatorBuild> nmake</pre>
6. Now go find something to do, because this will take some time.

## Compiling RubyCreator

You are closer... just a few minutes.

1. Open the MSVC2013 Developer Command Prompt and make sure qmake is on system path like you did to compile QtCreator.
2. Go to directory you clonned RubyCreator.
3. Change to the branch that match the QtCreator version (qtc-3.6 for QtCreator 3.6.x).
4. Compile it :-)
   <pre>C:\...\RubyCreator> cd ..
C:\...\> mkdir RubyCreatorBuild
C:\...\> cd RubyCreatorBuild
C:\...\RubyCreatorBuild> qmake QTC_SOURCE=..\QtCreator QTC_BUILD=..\QtCreatorBuild ..\RubyCreator\ruby.pro
C:\...\RubyCreatorBuild> nmake</pre>

The plugin is called `Ruby.dll`, you can find it somwwhere in the QtCreatorBuild among with other plugins, copy it to your QtCreator plugins directory, restart it and done.

## Conclusions

Need to compile the entire QtCreator to just compile a small plugin is a pain in the ass, life would be easier if QtCreator packages had the necessary bits to compile plugins.
