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
	<img src="{{ site.url }}/assets/pygments-logo.png" />
</figure>
I know that Rouge is the recommended highlighter for Jekyll, but there currently
is not a lexar for MQL.  Until I get to writing one I am currently using Pygments
to display code blocks with line numbering. Unfortunately using Pygments with line
numbering breaks my Jekyll layout and does not correctly allow for copying and pasting
of code.  Here is how I installed Pygments and how to fix the code block formatting.
