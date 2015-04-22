---
title: How to disable logging of asset pipeline (sprockets) messages in Rails.
author: Mohit Jain
layout: post



permalink: /2012/10/how-to-disable-logging-of-asset-pipeline-sprockets-messages-in-rails/
description: How to disable logging of asset pipeline (sprockets) messages in Rails.
keywords: logging,  sprockets
categories: tips-and-tricks
---

Quiet assets turn off assets pipeline log, kind of:

{% highlight ruby %}
Started GET "/assets/application.js?body=1" for 127.0.0.1 at 2012-02-13 13:24:04  0400
Served asset /application.js - 304 Not Modified (8ms)
{% endhighlight %}
There are two solutions for this:

##First solution ( preferred one ) is to install a gem i.e.
{% highlight ruby %}
gem 'quiet_assets', :group => :development
{% endhighlight %}
##Second solution (in case you don’t want to use gem ) is:

Place the following code in config/initializers/quiet_assets.rb and restart your server.
{% highlight ruby %}

if Rails.env.development?
  Rails.application.assets.logger = Logger.new('/dev/null')
  Rails::Rack::Logger.class_eval do
    def call_with_quiet_assets(env)
      previous_level = Rails.logger.level

      Rails.logger.level = Logger::ERROR if env['PATH_INFO'] =~ %r{^/assets/}
      call_without_quiet_assets(env)
    ensure
      Rails.logger.level = previous_level

    end
    alias_method_chain :call, :quiet_assets

  end
end
{% endhighlight %}
