---
title: Add Expires headers to the assets in ruby on rails.
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/addexpires-headers-to-the-assets-in-Ruby on Rails/
categories: optimization performance quick-solution Server tips-and-tricks
---

There are many ways to add expires headers to assets in specified [here][1], and [here][2].

 [1]: http://www.codebeerstartups.com/how-to-set-an-expires-header-in-apache/
 [2]: http://www.codebeerstartups.com/how-to-add-cache-control-expires-headers-to-images-content-served-by-s3/

One another way to add expires headers to assets in ruby on rails is:
{% highlight ruby %}
config.static_cache_control = "public, max-age=31536000"  # in production.rb file
{% endhighlight %}
in config.ru file
{% highlight ruby %}
require ::File.expand_path('../config/environment',  __FILE__)
use Rack::Deflater
run YourApplicationName::Application
{% endhighlight %}
This can be very helpful in case you want to add expiry headers to assets hosted on heroku.
