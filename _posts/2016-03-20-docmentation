---
layout: post
date: 2016-03-20 12:36
title: "Documentation - Configuration & First Steps"
description: Basic information about the Steve.
comments: false
category:
- docs
- help
tags:
- documentation
- steve
- jekyll
---

Ruby:
{% highlight ruby lineanchors %}
# graphic for hidden card
hidden = []
hidden[0] = '  ┌─────────┐'
hidden[1] = '  │░░░░░░░░░│'
hidden[2] = '  │░░░░░░░░░│'
hidden[3] = '  │░░░░░░░░░│'
hidden[4] = '  │░░░░░░░░░│'
hidden[5] = '  │░░░░░░░░░│'
hidden[6] = '  │░░░░░░░░░│'
hidden[7] = '  │░░░░░░░░░│'
hidden[8] = '  └─────────┘'

def clear
  system 'clear' # mac
  system 'cls' # windows
end

def build_hidden_card(player, hidden)
  hidden.each_index { |idx| player[idx] = hidden[idx] }
end

def build_shown_card(player, card, shown)
  shown.each_with_index do |line, idx|
    face = line.tr_s('XY', card[0..-2])
    face = face.gsub('10 ', '10').gsub(' 10', '10')
    face.tr!('S', SUIT[card[-1, 1].to_sym].to_s)
    player[idx] = "#{player[idx]}#{face}"
  end
end
{% endhighlight %}

MQL:
{% highlight mql lineanchors %}
int start(){
  Print("Hello World, This is a test of line wrapping. what happens to an exce")
  Comment("Hello World");
}
{% endhighlight %}


##### General Settings
* **name**: Your name.
* **job_title**: Your job title.
* **email**: Your email. There are two <code>>where</code> email is used. First, if you entered the email and you've activated **show_email** option the end result will be a visible social email icon in the sidebar. The second use of your email is when you do not set your own avatar. In this case your email is used by the gravatar plugin to automatically fetch your gravatar.
* **description**: Describe yourself with a couple of words.
* **avatar**: Write down the full path to the avatar <code>http://mysite.com/blog/assets/images/avatar.jpg</code>. If you comment this row, "Steve" checks if you have an email and shows your gravatar if you have any.
* **favicon**: Want a favicon? Enter the full path here. For example <code>http://mysite.com/blog/assets/favicon.ico</code>.
* **twitter_handler**: Add your Twitter username without the @. It will be used for [Twitter Cards](https://dev.twitter.com/cards/overview){:target="_blank"}. The default card type for "Steve" is [Summary Card with Large Image](https://dev.twitter.com/cards/types/summary-large-image){:target="_blank"}.
* **analytics_code**: Add your Google Analytics Tracking ID. Example ID: *UA-XXXXXXX-2*.
* **disqus**: Add your website shortname from Disqus.

**Important Note:** Keep in mind that **name**, **job_title**, **twitter_handler** and some of the post specific variables are used as default meta data in some cases.
