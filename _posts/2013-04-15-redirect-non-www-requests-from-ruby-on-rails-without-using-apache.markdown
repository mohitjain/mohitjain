---
layout: post
title: "Redirect Non-WWW Requests from ruby on Rails without using apache"
description: Redirect Non-WWW Requests from ruby on rails Rails without using apache like on heroku using using cloudflare
keywords: apache,  redirect non-www
date: 2013-04-15 01:18
categories: redirection, heroku
---

##Solution 1: Apache config file:

One solution is apache config file like I have explained [here](http://www.codebeerstartups.com/2012/10/complete-guide-to-setup-a-rails-server/).

{% highlight ruby %}

NameVirtualHost my_server_ip:80
<VirtualHost *:80>
ServerName example.com
RewriteEngine On
Redirect permanent / http://www.example.com
</VirtualHost>

{% endhighlight %}

<!--more-->

##Solution 2: Use Some Type of Rack Middleware

Another common approach is to use some type of Rack middleware to achieve the redirection

{% highlight ruby %}

class CanonicalRedirect

  def initialize(app)
    @app = app
  end

  def call(env)
    request = Rack::Request.new(env)
    if request.host.starts_with?("www.")
      [301, {"Location" => request.url.sub("//www.", "//")}, []]
    else
      @app.call(env)
    end
  end

  def each(&block)
  end

end

{% endhighlight %}

You'll also need to tweak the configuration in your application.rb file.

{% highlight ruby %}

config.autoload_paths += %W(#{config.root}/lib)
config.middleware.use "CanonicalRedirect"

{% endhighlight %}

##Solution 3: A Better Way: Use Rails3 Routing

Rails 3.0 offers a lot of cool new improvements to routing. I will recommend to read this [rails guides article](http://guides.rubyonrails.org/routing.html)

{% highlight ruby %}

Foo::Application.routes.draw do
  constraints(:host => /example.com/) do
	  root :to => redirect("http://www.example.com")
	  match '/*path', :to => redirect {|params| "http://www.example.com/#{params[:path]}"}
	end
end

{% endhighlight %}
