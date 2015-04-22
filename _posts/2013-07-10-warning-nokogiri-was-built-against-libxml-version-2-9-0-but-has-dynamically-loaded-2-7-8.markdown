---
layout: post
title: "WARNING: Nokogiri was built against LibXML version 2.9.0, but has dynamically loaded 2.7.8"
description: "WARNING: Nokogiri was built against LibXML version x.x.x, but has dynamically loaded y.y.y"
date: 2013-07-10 03:45
categories: nokogiri ruby-on-rails
---

Have you ever seen this message while the Rails was loading up?

> WARNING: Nokogiri was built against LibXML version x.x.x, but has dynamically loaded y.y.y

This will help you:

{% highlight ruby %}

	bundle exec gem pristine nokogiri

{% endhighlight %}
