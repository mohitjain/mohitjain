---
title: Change browser url in case of ajax request using HTML5 pushState
author: Mohit Jain
layout: post
comments: true
permalink: /2013/02/change-browser-url-in-case-of-ajax-request-using-html5-pushstate/
categories: quick-solution tips-and-tricks utilities
---

To change browser URL in case of ajax requests, just simply paste this code in your application.js file and all the things will be by itself in the compatible browsers.

{% highlight javascript %}

if (history && history.pushState){
  $(function(){
   $('body').on('click', 'a', function(e){
      $.getScript(this.href);
      history.pushState(null, '', this.href);
    });
    $(window).bind("popstate", function(){
      $.getScript(location.href);
    });
  });
}

{% endhighlight %}

For the limited set, you can change the attribute selector. In my case ie ‘a’ so it's cool for the whole website. [For more details][1] check [railscasts][1]

 [1]: http://railscasts.com/episodes/246-ajax-history-state
