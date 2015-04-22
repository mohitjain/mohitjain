---
title: Converting Ruby time function into a database friendly format to compare time.
author: Mohit Jain
layout: post
comments: true
permalink:  /2013/01/converting-ruby-time-function-into-a-database-friendly-format-to-compare-time/

categories: optimization  tips-and-tricks utilities
---

Use to_s(:db) to convert Ruby time function into a database friendly format to compare time.

{% highlight ruby %}
    Time.now.to_s(:db)
{% endhighlight %}
However, be careful if you have a timezone specified in Rails because the time will be stored in UTC in the database. You’ll need to specify that to do proper comparisons.

{% highlight ruby %}
    Time.now.utc.to_s(:db)
{% endhighlight %}
You can also use NOW() function in MySQL instead of generating the current time in Ruby.
