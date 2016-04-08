---
layout: post
title:  "KColorChooser ported to KF5"
tags: kde kf5
---

After almost 2 years I can say, “KDE, I'm back”. I used KDE3 during their entire life time, but KDE4 was horrible,
nothing worked well, the network manager applet was terrible and everything was a mess... plus slow as hell.

So in the meantime I was using a setup based on OpenBox plus many small applications, like the 90's, everything
worked well and ultra fast! But the need to open a terminal and learn how to use xrandr just to attach a
external monitor without a reboot was also horrible... so I gave a try to KDE5 and it seems way better than KDE4, ok, kwin still slow and causing a lot of pain with the default configuration, but things are getting better.

So... I tried to help KDE5 with something simple that would not waste my time spent in my pletora of pet projects, and the simple thing was a stupid application that I see myself using from time to time, KColorChooser, the application is nothing but a way to pick colors from screen, just that, so I ported it to KF5 :-), the application is really stupid so the port took some minutes, but the code review some weeks, here's it, if you know Qt you will notice that it is just a QColorDialog with an extra _help_ button.

![Project Manager](/postimages/20160408_kcolorchooser.png)

That's it, it will be released on KDE applications 16.04 IIRC :-)
