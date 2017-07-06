---
title: 'Rescue blocks don&#8217;t need to be tied to a &#8216;begin&#8217;'
author: Mohit Jain
layout: post
comments: true
permalink: /2012/11/rescue-blocks-dont-need-to-be-tied-to-a-begin/
categories: General optimization quick-solution tips-and-tricks
---
Rescue blocks don’t need to be tied to a ‘begin’ in rails :) Really nice to make code cleaner. Here is a quick example:

{% highlight ruby %}

def my_awesome_method
  begin
   # My awesome code...
  rescue
   # my rescue block ...
  end
end
{% endhighlight %}
can be written as:

{% highlight ruby %}

def my_awesome_method
   # My awesome code...
  rescue
   # my rescue block ...
end

{% endhighlight %}
