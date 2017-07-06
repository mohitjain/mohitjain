---
title: 'Dont use time_ago_in_words'
layout: post
comments: true
permalink: /2012/10/dont-use-time_ago_in_words/
description: Prefer now to use time_ago_in_words in ruby on rails.
keywords: performance,  optimizations
categories: Performance ruby-on-rails
---

Rails provides a helper method time\_ago\_in_words to display the distance between one time and now, like “5 minute ago”, it’s very useful.

##Before

{% highlight ruby %}
times_ago_in_words(comment.created_at)
{% endhighlight %}
It looks fine, but we have some room to improve.

*   Your servers have to calculate the time ago for each request, it wastes the cpu capability on server side, why not move the calculation to client side.
*   If we calculate the time ago on server side, it gets difficult to cache the page. e.g. after you create a comment, the time ago of the comment shows “5 seconds ago”, if you cache the page, the time ago still show “5 second ago” after 3 minute (depends on your cache strategy).

##Refactor

The solution is to use browser script like javascript. On server side, what you need is to pass the created or updated time instead of calculated time ago, then the javascript will calculate the time ago on client side.

{% highlight ruby %}
<abbr class="timeago" title="<%= comment.created_at.getutc.iso8601 %>">
  <%= comment.created_at.to_s %>
</abbr>
{% endhighlight %}

Here is a javascript solution based on [jquery][1] , of course, you can use other time ago js library.

{% highlight javascript %}
$("abbr.timeago").timeago();
{% endhighlight %}
Now, you save the server cpu capability and make your page easier to cache.

[1]: http://timeago.yarp.com/
