---
title: Accessing view methods in controller
author: Mohit Jain
layout: post
comments: true
categories: tips-and-tricks
---
A lot of time we need view methods in the controller for example: to show a link in flash message and we start writing HTML code in the controller using string concatenation, and it works perfectly fine. Here is the quick tip to make that code cleaner.

{% highlight ruby %}
  view_context.link_to("Show", @product)
{% endhighlight %}

Similarly you can access a lot of other methods too. Pretty nice and clean ;)
