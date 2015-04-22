---
title: Use pluck instead of collect in ruby on rails.
author: Mohit Jain
layout: post
categories: optimization performance quick-solution tips-and-tricks utilities
---

I have seen lot of people use collect in ruby on rails. For example:

{% highlight ruby %}
User.first.gifts.collect(&:id)# Bad smell.
{% endhighlight %}

Use pluck in case you just want to get id ie:

{% highlight ruby %}
User.first.gifts.pluck(:id)
{% endhighlight %}

## Explanation
‘pluck’ is on the db level. It will only query the particular field. [See this.][1]

 [1]: http://guides.rubyonrails.org/active_record_querying.html#pluck "pluck in ruby on rails"

When you do:

{% highlight ruby %}
User.first.gifts.collect(&:id)
{% endhighlight %}

<!--more-->

You have objects with all fields loaded and you simply get the ‘id’ thanks to the method based on Enumerable.

So:

*   if you **only** need the ‘id’, use ‘pluck’
*   if you need **all** fields, use ‘collect’
*   if you need **some** fields, use ‘select’ and ‘collect’

So keep in mind when to use pluck instead of collect in ruby on rails.
