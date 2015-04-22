---
layout: post
title: "Dummy SMTP for emails testing on heroku"
date: 2013-04-14 15:03
description: How to test emails on heroku.
keywords: email testing, heroku, fake smtp, fake emails
categories: testing development ruby-on-rails
---

Looking for a solution for email testing on heroku. [Mailtrap](http://mailtrap.io/) is a solution released by [railsware](http://railsware.com/). Here is how you can use it.

##Installation

{% highlight ruby %}

heroku addons:add mailtrap

{% endhighlight %}

<!--more-->


Once installed you can see settings for the same ie MAILTRAP_HOST, MAILTRAP_PORT, MAILTRAP_USER_NAME, MAILTRAP_PASSWORD by running a command ie:

{% highlight ruby %}

heroku config -s | grep MAILTRAP

{% endhighlight %}

Paste these lines of code in you environment file.

{% highlight ruby %}

if ENV['MAILTRAP_HOST'].present?
  ActionMailer::Base.delivery_method = :smtp
  ActionMailer::Base.smtp_settings = {
    :user_name => ENV['MAILTRAP_USER_NAME'],
    :password => ENV['MAILTRAP_PASSWORD'],
    :address => ENV['MAILTRAP_HOST'],
    :port => ENV['MAILTRAP_PORT'],
    :authentication => :plain
  }
end

{% endhighlight %}
Now you are all set. Go ahead and start testing your emails without actually sending them to your real customers ;)

Note: I am using [mailcatcher](http://www.codebeerstartups.com/2013/01/how-to-test-emails-in-development-mode-in-Ruby on Rails/) to test emails on development machine. You must give it a try





