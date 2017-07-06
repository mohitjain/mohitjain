---
title: Use rescue to rescue in ruby on rails
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/use-rescue-to-rescue-in-Ruby on Rails/
categories: optimization performance quick-solution tips-and-tricks
---
In case you know the code can crash use rescue. An exclusive use of rescue to rescue is:

## Before

{% highlight ruby %}
a = nil
a.a_random_method_call # code will crash here
{% endhighlight %}

## After

{% highlight ruby %}

a = nil
a.random_method_call rescue "Handling the fallback."
#, in this case, it will only return "Handling the fallback."
{% endhighlight %}
Pretty nice.
