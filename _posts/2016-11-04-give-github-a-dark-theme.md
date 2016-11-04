---
layout: post
date: 2016-11-04 11:48
title: "Use Stylish To Save Your Retinas From A Bright GitHub"
description: Use the Stylish extension to apply a theme to GitHub and other sites.
comments: true
category:
- how-to
tags:
- github
- how-to
---
<figure class="alignleft">
	<img src="{{ site.image }}light_to_dark.png" width="120"/>
</figure>
I use the One Dark theme in Atom and the Solarized Dark theme in iTerm2 since they
are both easier on the eyes than a lighter theme. Many popular sites, GitHub included,
sport a light colored theme and while this may suit casual users of these sites, if
you spend a bit of time the lighter colors seem to cause a bit of eyestrain and in
many cases fatigue. Using the browser extension, Stylish, you can apply a user theme
to many popular sites and web applications.

Stylish is available for Chrome, Firefox, Safari and Opera and allows one to apply
user supplied style sheets to a web page. While you can create your own for any
website, [userstyles.org](http://userstyles.org) has over 76,000 site styles, over
5,000 app styles and over 7,000 global styles available.

### How to turn Github to a darker style
Here is how I changed the look of GitHub on my machine from this:
<img src="{{ site.image }}github_before.jpg" />
to this:
<img src="{{ site.image }}github_after.jpg" />
I used the [GitHub Dark 2.0](https://userstyles.org/styles/128271/github-dark-2-0)
theme from userstyles.org. Visit the link above and if you do not have Stylish installed
there will be a link to install Stylish. If you already have Stylish installed you
will be provided with a link to install the theme.

On inital install of this theme, this style will be applied to every website.  To
make this only apply to GitHub you need to edit the style. On the bottom of the
page for editing the style (below the css), you will see this section:
<img src="{{ site.image }}stylish_before.jpg" />
You need to change it so that it applies this style to all URLs on the domain github.com,
as follows.  Make sure to press save in the upper left hand corner of the page to apply
the rule.
<img src="{{ site.image }}stylish_after.jpg" />
Now you have a GitHub experience that is a little easier on the eyes.  Applying
styles to additional sites is just as simple.  I for one have change YouTube to a
darker style.
