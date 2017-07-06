---
title: Interpolate text quickly in ruby
author: Mohit Jain
layout: post
comments: true
permalink: /2012/11/interpolate-text-quickly-in-ruby/
categories: General quick-solution tips-and-tricks
---

You could store a format string:

{% highlight ruby %}
my_string = "Congrats, you have joined %s"
group_name = "My Group"
puts my_string % group_name # prints: Congrats, you have joined My Group
{% endhighlight %}
For multiple variables in the same string you can use
{% highlight ruby %}
my_string = "Congrats, you have joined %s and %s"
group_name = ['group1', 'group2']
puts my_string % ['group1', 'group2']  # prints: Congrats, you have joined group1 and group2
{% endhighlight %}
A nice to Interpolate text quickly in ruby.
