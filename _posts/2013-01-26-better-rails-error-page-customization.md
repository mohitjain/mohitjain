---
title: Better Rails error page customization, display more information
author: Mohit Jain
layout: post
permalink: /2013/01/better-rails-error-page-customization/



categories: quick-solution tips-and-tricks utilities
---

Rails error page customization is much easier using [Better Errors][1] gem which replaces the standard Rails error page with a much better and more useful error page. Pretty nice gem.

 [1]: https://github.com/charliesome/better_errors

All you need is add a single gem in your gemfile.
{% highlight ruby %}
gem "better_errors"
{% endhighlight %}

Run bundler and restart your server.

**Sample:**

![Sample error page](/wp-content/uploads/2013/01/Screen-Shot-2013-01-26-at-2.22.25-AM.png?fit=1264,681)
