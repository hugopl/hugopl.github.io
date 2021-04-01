---
layout: post
title:  "GTK3/Gnome Custom Keyboard Compose Sequences"
tags: Gtk keyboard accents
---

For personal historical reasons I'm used to US keyboards, so to write portuguese text with those keyboards I need to use the `English (US, int. with dead keys)` layout that provides compose sequences to write characters like `áàãéíóóõúüç`.

To generate a `'` character I type <kbd>'</kbd> + <kbd>&nbsp;&nbsp;&nbsp;&nbsp;</kbd>. It's this way since ever.... but lately (starting from GTK3 version 3.24.28) somebody decided that this was a bug, not a feature. If someone type this compose sequence the generated character should be `´`, not `'`, and to generate `'` you would need to type <kbd>AltGr</kbd> + <kbd>'</kbd>. The problem is that in protuguese the character `´` alone have no meaning/usage, on the other hand the character `'` is used a lot when programming, i.e. this had a huge impact on me.

Long story short, to let GTK behave like I'used to, create a file named `.XCompose` on your home directory with this:

```
<dead_acute> <space>                : "'"   apostrophe # APOSTROPHE
```

If you are not used to the XCompose format, check `/usr/share/X11/locale/en_US.UTF-8/Compose` and you are going to have a idea (or _man 5 Compose_).

In the past the behavior change that made a headache was <kbd>'</kbd> + <kbd>c</kbd> generating `ć` instead of `ç` as I was used to, the new compose sequence (that now I'm used to) is <kbd>AltGr</kbd> + <kbd>,</kbd>. Hope it helps whoever is reading.
