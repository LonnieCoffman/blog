---
layout: post
date: 2016-10-24 14:05
title: "My Jekyll Blog 2: Keeping Pygments from Breaking Jekyll"
description: How to use css to keep pygments from breaking jekyll when using line numbers.
comments: true
category:
- How-To
tags:
- ruby
- jekyll
- jekyll blog
---
<figure class="alignleft">
	<img src="{{ site.url }}/assets/pygments-logo.png" width="120"/>
</figure>
I know that Rouge is the recommended highlighter for Jekyll, but there currently
is not a lexar for MQL.  Until I get to writing one I am currently using Pygments
to display code blocks with line numbering. Unfortunately using Pygments with line
numbering breaks my Jekyll layout and does not correctly allow for copying and pasting
of code.  Here is how I installed Pygments and how to fix the code block formatting.

### Install Pygments on Mac OS for use in Jekyll

Installing Pygments on the mac is as simple as running the following two commands.
{% highlight console %}
 ~ $ sudo easy_install Pygments
 ~ $ gem install pygments.rb
{% endhighlight %}

Then within the <code>_config.yml</code> file change the highlighter from rouge to pygments.

{% highlight js lineanchors %}
highlighter: pygments
{% endhighlight %}

In the gemfile add pygments.rb to the group section as in the example codeblock below.

{% highlight js lineanchors %}
group :jekyll_plugins do
	gem 'jekyll-paginate'
	gem 'jekyll-sitemap'
	gem 'pygments.rb'
end
{% endhighlight %}

Now all there is to do is update

{% highlight console %}
 ~ $ bundle install
{% endhighlight %}

### How to fix the layout and add linenumbers

I used [Drew Silcock's solution](https://drewsilcock.co.uk/proper-linenumbers) as
a starting point and modified it to suit my needs.

I modified the highlight class in <code>assets/partials/_syntax.scss</code> to the following
for the general layout of my codeblocks.

{% highlight css lineanchors %}
.highlight { background: #282C34;
             border-radius: 10px;
             border: 3px solid #ccc;
             padding: 15px 10px 15px 2px;
             color: #eee;
             font-size: 15px;
             text-shadow: 0 1px rgba(0,0,0,0.2);
             -webkit-font-smoothing: antialiased !important;
             -moz-osx-font-smoothing: grayscale;
{% endhighlight %}

Then I added the following to produce unselectable line numbers using
[CSS counters](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters)
and then styled the scrollbars to fit the codeblocks better.

{% highlight css lineanchors %}
::-webkit-scrollbar {
  width: 14px;
  height: 24px;
}
::-webkit-scrollbar-thumb {
  margin: 0 10px;
  border: 8px solid rgba(0, 0, 0, 0);
  background-clip: padding-box;
  -webkit-border-radius: 18px;
  background-color: #484848;
  -webkit-box-shadow: inset -1px -1px 0px rgba(0, 0, 0, 0.05), inset 1px 1px 0px rgba(0, 0, 0, 0.05);
}
::-webkit-scrollbar-track {
  margin: 0 36px;
}
::-webkit-scrollbar-button {
  width: 0;
  height: 0;
  display: none;
}
::-webkit-scrollbar-corner {
  background-color: transparent;
}

a {
  border: 0;
}

pre {
  counter-reset: line-numbering;
  padding: 0;
  white-space: pre;
  overflow-x: auto;
  word-break: inherit;
  word-wrap: inherit;
}

pre a::before {
  content: counter(line-numbering);
  counter-increment: line-numbering;
  padding-right: 5px; /* space after numbers */
  width: 22px;
  text-align: right;
  display: inline-block;
  color: #999;
  background: #282C34;
  margin-right: 16px;
  border-right: 1px solid #666;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
{% endhighlight %}

Finally, within <code>assets/css/main.scss</code>, in order to prevent longer lines from breaking, I had to change the white-space
property within the code class to pre as in the following line.

{% highlight css lineanchors %}
code, kbd, pre { margin: 0;
                 line-height: 20px;
                 font-family: Consolas, Monaco, 'Andale Mono', 'Ubuntu Mono', monospace;
                 word-wrap: break-word;
                 word-break: break-word;
                 white-space: pre; }
{% endhighlight %}

### How to display a codeblock with line numbers

You now have Pygments installed and not breaking your Jekyll layout. In order to display
a codeblock with you given code along with line numbers use the ruby example below.
To omit linenumbers simply leave out the lineanchors parameter.

{% highlight text %}
  { % highlight ruby lineanchors % }
   puts 'my amazing ruby code'
   puts 'yet even more code'
  { % endhighlight % }
{% endhighlight %}
