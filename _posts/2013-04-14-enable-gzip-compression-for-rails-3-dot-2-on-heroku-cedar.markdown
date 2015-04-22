---
layout: post
title: "Enable gzip compression for Rails 3.2 on heroku Cedar"
description: Enable gzip compression for Rails 3.2 on heroku Cedar
keywords: heroku, gzip compression
date: 2013-04-14 15:33
categories: heroku ruby-on-rails
---

The simplest way to enable gzip compression in Rails 3.2 is by adding “use Rack::Deflater” in config.ru file.

{% highlight ruby %}

# This file is used by Rack-based servers to start the application.

require ::File.expand_path('../config/environment',  __FILE__)
use Rack::Deflater
run Improvingoutcomes::Application

{% endhighlight %}
