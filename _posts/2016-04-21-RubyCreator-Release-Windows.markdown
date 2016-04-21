---
layout: post
title:  "RubyCreator release and Windows binaries!"
tags: ruby rubycreator qt msvc2013 windows
---

If you have a Windows 32bits and want to try RubyCreator I present you the first RubyCreator binary distribution!

Only Windows 32bits is available since I only have a Windows7 32bits VM available. Consider the Windows distribution beta, I don't test/use it everyday like I do with the Linux version.

![Project Manager](/postimages/20160421-win-rubycreator.png)

This hand in the screenshot is from my Linux desktop and I'm too lazy to go there take another shot, since I compiled and tested using a VM.

I turned off font anti aliasing, with it on I was not able to proper see the bold text used in RubyCreator sintaxhighlighter, I also didn't test the Rubocop integration, but it should work, to try it: Add ruby to the system path and make the rubocop gem available for it.

To install it go to [Github](https://github.com/hugopl/RubyCreator/releases) releases page, download the zip file, unzip and copy the `Ruby.dll` file to the QtCreator plugins directory. Restart QtCreator and done.

The binary distribution is GPG signed (.sig file) if some nerd want to check if was really me that created it, BTW I need create a new GPG key, mine is too old.

## Want a 64bits version?

So help me, I wrote instructions about how to [compile the plugin on Windows]({% post_url 2016-04-20-Compiling-RubyCreator-on-Windows %}), it's not that hard but takes some time.

## Conclusions

After too many years without code a single hello world on Windows I have the feeling that Courrier New font is very ugly, but ok, it works.
