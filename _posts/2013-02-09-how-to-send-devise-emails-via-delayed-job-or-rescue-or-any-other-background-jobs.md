---
title: How to send devise emails via delayed job or rescue or any other background jobs
author: Mohit Jain
layout: post
comments: true
permalink: /2013/02/how-to-send-devise-emails-via-delayed-job-or-rescue-or-any-other-background-jobs/
categories: optimization performance tips-and-tricks
---


All always prefer to use [devise][1] in my application. But the problem is emails. Devise send emails synchronously but if you want to send then asynchronously here is a quick tip for you. Use [devise-async][2] gem.

 [1]: https://github.com/plataformatec/devise "Devise gem"
 [2]: https://github.com/mhfs/devise-async

## Installation

{% highlight ruby %}

gem 'devise-async'

{% endhighlight %}

<!--more-->

Now enable module in your model ie

{% highlight ruby %}

class User < ActiveRecord::Base
  devise :database_authenticatable, :async, :confirmable # etc ...
end

{% endhighlight %}

By default devise-asyn use resque so if you are not using resque then set your queuing backend by creating config/initializers/devise_async.rb:

{% highlight ruby %}

# Supported options: :resque, :sidekiq, :delayed_job, :queue_classic
Devise::Async.backend = :delayed_job

{% endhighlight %}

Thats it. Now this will send all the devise emails via delayed job or rescue or any other background jobs.

Make sure your devise-asyn gem is below devise gem else you will get an error like:

{% highlight ruby %}

/Users/me/.rvm/gems/custom_gem_set/gems/devise-async-0.5.1/lib/devise/async.rb:47:in `': undefined method `add_module' for Devise:Module (NoMethodError)

{% endhighlight %}
