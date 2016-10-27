---
layout: post
date: 2016-10-22 12:50
title: "Fix Unknown Ruby Interpreter Version in Jekyll"
description: How to fix Unknown ruby interpreter version (do not know how to handle) RUBY_VERSION and RVM warning.
comments: true
category:
- How-To
tags:
- rvm
- jekyll
- jekyll blog
---
<figure class="alignleft">
	<img src="{{ site.url }}/{{ site.baseurl }}/assets/terminal_warning.jpg" />
</figure>
When setting up a new Jekyll site while using RVM I get a warning message about
RVM using my Gemfile for selecting Ruby.  In addition another warning is displayed
that states that it does not know how to handle "Unknown ruby interpreter version".
Although no issues (that I am aware of) will be encountered by leaving this as is,
I prefer to not have to view these messages every time that I work on the files
in this directory. So, here is how to remove the warnings and fix the RUBY_VERSION
error.

These are the error messages that I receive.

{% highlight text %}
 RVM used your Gemfile for selecting Ruby, it is all fine - Heroku does that too,
 you can ignore these warnings with 'rvm rvmrc warning ignore /Users/lonnie/development/blog/Gemfile'.
 To ignore the warning for all files run 'rvm rvmrc warning ignore allGemfiles'.

 Unknown ruby interpreter version (do not know how to handle): RUBY_VERSION.
{% endhighlight %}

### Prevent RVM warning from displaying
The RVM warning message above displays the instructions for removing the warning.
In my case all that I needed to do was enter the following in a terminal.

{% highlight sh %}
rvm rvmrc warning ignore /Users/lonnie/development/blog/Gemfile
{% endhighlight %}

### Fix unknown ruby interpreter version

To remove the 'Unknown ruby interpreter version' message we first need to find
the version number of Ruby that is currently running.  An easy way to do this
is by:

{% highlight sh %}
env | grep 'RUBY'
{% endhighlight %}

This gives me the following information from which I can see that I am using Ruby
2.3.0.

{% highlight text %}
 MY_RUBY_HOME=/Users/dad/.rvm/rubies/ruby-2.3.0
 RUBY_VERSION=ruby-2.3.0
{% endhighlight %}

As you can see the RUBY_VERSION environment variable is set to 'ruby-2.3.0' whereas
Jekyll is expecting it to simply be '2.3.0'. So, to fix this we simply need to change
the line in our Jekyll gemfile that reads <code>ruby RUBY_VERSION</code> to
<code>ruby '2.3.0'</code>
