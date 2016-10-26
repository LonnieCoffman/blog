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

##### 2. Create a folder for your new site
Since I am installing a blog I am going to create a folder named 'blog' to store
all of the site files in.
{% highlight console %}
 ~ $ mkdir blog
{% endhighlight %}

##### 3. Navigate to the folder you just created
Change to the 'blog' directory that you just created.
{% highlight console %}
 ~ $ cd blog
{% endhighlight %}

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
Copy all of the template files to the folder created in step 3. In my case this
is the blog folder. The <code>_config.yml</code> file contains specific settings for
your site, so it will need to be edited. Finally we need to setup Jekyll and all of
it's dependencies by issuing the following command.
{% highlight console %}
 ~/blog $ bundle install
{% endhighlight %}

##### 6. View and edit your new blog

You can view the site that Jekyll just created on a local server. Change to the
blog directory that you just created and
enter the following.
{% highlight console %}
 ~ $ bundle exec jekyll serve
{% endhighlight %}
