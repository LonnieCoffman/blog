---
layout: post
date: 2016-10-21 16:25
title: "My Jekyll Blog 1: Local Installation and Initial Setup"
description: How I set up a local Jekyll install to develop my blog offline while learning about Jekyll and how to configure it
comments: true
category:
- How-To
tags:
- pygments
- jekyll
- jekyll blog
---

<figure class="alignleft">
	<img src="{{ site.url }}/assets/sm_jekyll.png" />
</figure>
My ongoing adventure in setting up and customizing a <a href="http://jekyllrb.com" title="Title">Jekyll</a> blog.  In this First
post I go over a little about Jekyll, why I chose it instead of Wordpress or other
:sparkles:shiny options, How to install it and load a theme from the web.

### What is Jekyll?
Jekyll is *"a simple, blog aware, static site generator"* provided as a Ruby Gem.
This means that using your favorite text editor (mine's [Atom]({{ site.url }}/tag/atom))
you can create and maintain a simple static blog or other website. Jekyll uses
markup language for content which really makes it simple to format content.

### Why I chose to use Jekyll
My reasons for choosing Jekyll for this blog are two-fold.

First I wanted to keep things simple and reliable. Unlike most blogging platforms
there are no databases to maintain and no constant updates to keep up with. This
frees up more time for content creation.

Secondly, since I am currently learning Ruby at [Launch School](http://launchschool.com)
and using GitHub on a daily basis I thought that this would be a great way to
expand my knowledge of both at the same time.

### How to install Jekyll locally
As a note, I am installing on Mac OS and already have Ruby installed and am not
using GitHub Pages for site updates.

##### 1. Install the Jekyll and Bundler gems.
{% highlight console %}
 ~ $ gem install jekyll bundler
{% endhighlight %}

##### 2. Create a new Jekyll installation
Instruct Jekyll to create a new installation using the following command. In this example
we are going to create the installation in a folder named 'blog'. If this folder
does not exist it will be created automatically.
{% highlight console %}
 ~ $ jekyll new blog
{% endhighlight %}

##### 3. Navigate to the folder you just created
Change to the 'blog' directory that you just created.
{% highlight console %}
 ~ $ cd blog
{% endhighlight %}

##### 3a. (Optional) Remove warning message
I use RVM and get the following message. It does not cause any issues and you are
safe to ignore it.
{% highlight console %}
 RVM used your Gemfile for selecting Ruby, it is all fine - Heroku does that too,
 you can ignore these warnings with 'rvm rvmrc warning ignore /Users/Lonnie/Development/blog/Gemfile'.
 To ignore the warning for all files run 'rvm rvmrc warning ignore allGemfiles'.

 Unknown ruby interpreter version (do not know how to handle): RUBY_VERSION.
{% endhighlight %}

If you would like to fix this read on, otherwise skip to step 4.

To remove the RVM warning message input the line that was listed in the message.
Based on the message I would enter the following:
{% highlight console %}
 ~/blog $ rvm rvmrc warning ignore /Users/Lonnie/Development/blog/Gemfile
{% endhighlight %}

To remove the 'Unknown ruby interpreter version' message we first need to find
the version number of Ruby that we are currently running.  An easy way to do this
is by:
{% highlight console %}
 ~/blog $ env | grep 'RUBY'
{% endhighlight %}
This gives me the following information from which I can see that I am using Ruby
2.3.0.
{% highlight console %}
 MY_RUBY_HOME=/Users/dad/.rvm/rubies/ruby-2.3.0
 RUBY_VERSION=ruby-2.3.0
{% endhighlight %}
As you can see the RUBY_VERSION environment variable is set to 'ruby-2.3.0' whereas
Jekyll is expecting it to simply be '2.3.0'. So, to fix this we simply need to change
the line in our Jekyll gemfile that reads <code>ruby RUBY_VERSION</code> to
<code>ruby '2.3.0'</code>

##### 4. Get a template
One of the great things about Jekyll is that there are many templates available
to get you up and running quickly. Most are few are cost very little. Here are a few
resources for templates:

* [Search for Jekyll Themes on GitHub](https://github.com/search?utf8=%E2%9C%93&q=jekyll+theme)
* [Jekyll Wiki Page on GitHub](https://github.com/jekyll/jekyll/wiki/Themes)
* [JekyllThemes.org](http://jekyllthemes.org/)
* [JekyllThemes.io](https://jekyllthemes.io/)
* [Theme Forest](https://themeforest.net/category/static-site-generators/jekyll)

In addition, there are many Gem-based themes. Since I installed a downloaded theme
that I purchased from Theme Forest, the rest of this post will focus on how I
installed it.

##### 5. Install your template
WIP

##### 6. View and edit your new blog

You can view the site that Jekyll just
created on a local server. Change to the blog directory that you just created and
enter the following.
{% highlight console %}
 ~ $ bundle exec jekyll serve
{% endhighlight %}
