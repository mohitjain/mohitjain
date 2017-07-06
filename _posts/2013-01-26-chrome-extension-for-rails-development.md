---
title: Chrome extension for Rails development
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/chrome-extension-for-rails-development/
categories: optimization performance quick-solution tips-and-tricks utilities
---

I was browsing the web and came to know about a Chrome extension for Rails development[RailsPanel][1] which display some of the good logging information in a good manner.

 [1]: https://chrome.google.com/webstore/detail/railspanel/gjpfobpafnhjhbajcjgccbbdofdckggg

**Setup guidelines:**


*   Install the Chrome extension [RailsPanel][1]
*   Install the gem which passes the meta tags

{% highlight ruby %}
group :development do
 gem'meta_request','0.2.1'
end
{% endhighlight %}
**Sample**
![Rails Panel Chrome Extension for Rails logging](/wp-content/uploads/2013/01/railspanel.png?fit=1236,778)
