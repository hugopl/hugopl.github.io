---
layout: post
title:  "Display Ruby version on prompt"
tags: Ruby bash
---

The problem: I have multiple versions of Ruby installed and want to be sure about what version is the default on a terminal session.

Solution: Display the version on prompt!

I already do it for git branches, to show Ruby version is even simpler, on your `.bashrc`...

{% highlight bash %}
RUBYVERSION='$(ruby --version | cut -f2 -d\ )'
PS1="\u \w [${RUBYVERSION}] \$ "
{% endhighlight %}

Of course you will change the PS1 to fit your needs with colors, etc... or your prompt will be pretty gray and ugly, BTW here is mine:

{% highlight bash %}
RUBYVERSION='$(ruby --version | cut -f2 -d\ )'
GITPS1='$(__git_ps1 "(%s)")'
PS1="\033[01;32m\u\033[0m \w \033[31m${GITPS1}\033[0m \033[35m[${RUBYVERSION}]\033[0m\n\$ "
{% endhighlight %}
