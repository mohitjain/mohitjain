---
layout: post
description: How to Set the default time zone for a Heroku app
title: "How to Set the default time zone for a Heroku app"
date: 2013-04-19 01:53
keywords: heroku, timezone, default timezone
categories: heroku server
---

For Rails apps running on Heroku, by default Time.now and some_time.localtime will display in UTC. If you’d like to assign a time zone to your app, you can set the TZ config variable to a time zone (which must be in the [tz database timezone](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones) format).

Personally, I despise the tz database format, because it requires you to guess WHICH city is chosen to represent that time zone (for Pacific, it’s Los_Angeles, not Seattle, not San_Francisco). But that’s what Heroku uses, so to set your app to Pacific you simply run:

{% highlight ruby %}

  heroku config:add TZ="America/Los_Angeles"

{% endhighlight %}

The allowed options are listed on the page linked above.
