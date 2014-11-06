---
layout: post
title:  "Code review tools and git workflow"
tags: git reviewit
---

If you are not alone on a project you probably have some kind of code review, if it's not explicit at least someone will at some point see what you did and blame it.

There are plenty of code review tools out there, free, non free, too much simple, too much complex, etc... most of them didn't attended my point of view of what a code review tool should be. In my point of view any tool should be just a tool, any good developer is too busy with the problems it must solve to waste time configuring, learning, using tools, tools should exists to help not to create yet another thing to worry about.

This doesn't mean all other code review tools are shitty, phabricator is a nice one, gerrit fit on some more complex workflows, etc... but let me introduce what *my* code review tool have:

## An ugly logo
<img src="/postimages/20141106_reviewit_logo.png" alt="Review it!" class="flat">

...and a name: *Review it!*.

## Simple Web interface, just for code review, nothing more

The web interface is super simple, it allows you to see the various versions of the patch, accept, reject of comment on patch lines. Just this.

Accepted patches go to the git repository without need of any extra manual step.

## Simple CLI interface for simple things

Send a merge request is a matter of type <code>review push master</code>, this mean: "Push the git commit on HEAD for review targeting the master branch."

To update a merge request is even easier, <code>review push</code>.

See pending reviews? <code>review list</code>.

Open a merge request on your browser? <code>review open ID</code>.

Apply a merge request patch on your tree? <code>review apply ID</code>

Show a merge request patch without open the browser? <code>review show ID</code>

Oops, want to cancel a merge request? <code>review cancel ID</code>

The idea is simple, simple commands for simple things.

## (almost) Zero configuration needed

To configure the CLI is also much simpler, go to the Web interface, copy and paste the command on your terminal (in the project directory), something like

$ <code>curl http://myniceurl.com/api/projects/1/setup?api_token=yes9PHCXRACsOf2lM79_cA | ruby</code>

This will set some keys to your project .git/config and install a ruby gem if needed.

## TODO list

I would like to have some kind of CI and Lint integration soon.

## Where to get it?

Github! Check the <a href="https://github.com/hugopl/reviewit">github page</a>.
