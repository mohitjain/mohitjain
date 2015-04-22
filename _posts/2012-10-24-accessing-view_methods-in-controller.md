---
title: Accessing view methods in controller
author: Mohit Jain
layout: post
comments: true

permalink: /2012/10/accessing-view_methods-in-controller/
categories: tips-and-tricks
---

Lot of time we need view methods in controller for example: to show a link in flash message and we start writing html code in controller using string concatenation, and it works perfectly fine. Here is the quick tip to make that code more cleaner.

{% highlight ruby %}
view_context.link_to("Show", @product)
{% endhighlight %}
Similarly you can access a lot of other methods too. Pretty nice and clean ;)
