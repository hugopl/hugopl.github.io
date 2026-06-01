---
layout: post
title:  "Why did I try to write my own code editor?"
tags: opensource
---

I've been doing pet projects since I started programming computers more than 20 years ago 👴🏽️, besides learning a lot from these pet
projects, they give me joy. I'm used to saying that _”Coding pet projects is my video game”_.

But pet projects are only worth it if you use them, otherwise it's an experiment, etc... something that will last for a few weeks
and you move on to another thing of interest to have fun.

I used to write ruby code on QtCreator using a [ruby language plugin](https://github.com/hugopl/RubyCreator), the problem is
that I do not enjoy coding in Qt/C++ as I did some years ago, so maintaining this plugin up to date for every QtCreator API change
was a pain. Long story short: Pet project archived and now I was in need for a code editor to write Ruby code.

In 2019 I fell in love with [Crystal language](https://crystal-lang.org/) ❤️ it had the good things I love from Ruby and the good things I missed from typed
and compiled languages like C++. At the time there weren't many choices to code in Crystal besides the slow VSCode and the
generic non-free Sublime3.

Some experimental GObject binding generator existed, so it was possible to create GTK applications in Crystal, then
I thought: why not create a code editor in GTK the way I want to!?

<img src="/postimages/20230601_blackjack.jpg" alt="Futurama meme!" class="flat">

## Tijolo was born 🧱️

I named it <a href="https://github.com/hugopl/tijolo">Tijolo</a>, means _brick_ in Portuguese, and started the project
somewhere in 2019.

I wanted Tijolo to be very fast like terminal editors, easy to work with split
views like my terminal at the time
([Tilix](https://gnunn1.github.io/tilix-web/)) and keyboard focused.

With [LSP](https://microsoft.github.io/language-server-protocol/) and [GtkSourceView](https://wiki.gnome.org/Projects/GtkSourceView)
I just needed to glue everything together with some Crystal code, easy like that.

However when I got around the version 0.7.0 I realized a list of problems with the project:

- Current GTK bindings had memory leaks, problems with Crystal GC and only supported GTK3.
- GTKSourceView API would make some of my ideas for the future harder to implement, besides the problem opening big files.

So I decided to rewrite Tijolo, the new Tijolo would:

- Be written in Crystal, the language that most bring me joy to code nowadays.
- Use GTK4 and don't leak memory, so another pet project was born, <a
    href="https://github.com/hugopl/gi-crystal">GI-Crystal</a>, a GObject
binding generator.
- Write my own code editor widget instead of using GtkSourceView.
- Syntax highlighting would be backed by tree-sitter, so <a
    href="https://github.com/hugopl/crystal-tree-sitter">crystal-tree-sitter</a>
was born.

So far this plan is on track, however far away from an end.

- I created a GObject binding generator.
- I created nice GTK4 bindings using that generator.
- I created tree-sitter bindings.
- Tijolo GTK3 was simplified and ported to GTK4.
- I started to work on a primitive editor widget.
- I started to write a PieceTable shard to be used as the buffer of the editor widget.
- Then I started to realize the obvious, it was too many things to do for my free time.

Long story short, I decided to learn vim for the third time, but this time with
more seriousness. I started the migration to neovim in December 2025 where
things are more calm at work and it worked, since then I've been a happy neovim <3
user.

## Conclusion

A few things happened.

- From tijolo way of handling editor views,
[Batata](http://github.com/hugopl/batata) was born, it's like a Tilix, I wrote
it because there was no GTK4 version of Tilix.
- My GTK4 bindings are being used by some people, it's good for the ego to
know someone is using your code.
- I learned a lot about GTK, GObject and tree-sitter, a knowledge that I doubt
will be useful in my professional life, but is always fun to know.
- I wrote [RTFM](http://github.com/hugopl/rtfm), a GTK application used to read
documentation in the dash format, I use it every day to read Crystal docs.
- I had kids (twins) and all my free time is gone.


