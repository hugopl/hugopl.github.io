---
layout: post
title:  "Embedding Ruby 2.1 into a C++ application"
tags: ruby
---

I'm writing this as a reminder to myself, first of all  because there is no documentation about how to embedded Ruby into a C++ application besides the Ruby interpreter source files, secondly because when you start a sentence saying "first.." you need a second sentence saying "secondly...".

The fast way to explain what you need to do:

{% highlight cpp %}
#include <ruby.h>

int main()
{
    // Init ruby VM.
    ruby_init();
    // You need this if you plan to load some modules using require.
    ruby_init_loadpath();

    const char*  options[]  =  { "", "-enil", 0 };
    ruby_exec_node(ruby_options(2, const_cast<char>(options)));

    const char rubyCode[] = "my nice ruby code here";
    int result;
    rb_eval_string_protect(rubyCode, &result);
    if (result)
        return 1; // An exception was thrown.

    ruby_cleanup(0);
    return 0;
}
{% endhighlight %}

`ruby_options` receive argc/argv as parameters, they are used like the Ruby interpreter would do, a void pointer is returned. The void pointer returned is a Node, it represents the Ruby code compiled and ready to run.

Notice _"-enil"_, if you don't pass any argument the Ruby VM will crash without further explanation. In my example I want to execute some Ruby code located into a string, not a separated file, so I can't pass the file path into options array because there's no file, so _-enil_ says _"Execute this code: 'nil'"_.

You can use the void pointer returned by `ruby_options` into two functions, `ruby_run_node` and `ruby_exec_node`, the difference is that `ruby_run_node` executes the node then clean up the VM, so any other call to the Ruby C-API will cause a crash, `ruby_exec_node` just execute the node and keeps the VM alive for a future use.

Now with all in place, you can call `rb_eval_string_protect` to execute some ruby code and all other `rb_`* functions found on ruby.h to do whatever do you want, at least those `rb_`* functions have some documentation into <a href="https://github.com/ruby/ruby/blob/trunk/README.EXT">README.EXT</a> file found on Ruby source code.