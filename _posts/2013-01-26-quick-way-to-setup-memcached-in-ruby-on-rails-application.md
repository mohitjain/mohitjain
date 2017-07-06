---
title: Quick way to setup memcached in Ruby on Rails application
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/quick-way-to-setup-memcached-in-Ruby on Rails-application/
categories: optimization performance quick-solution Server tips-and-tricks
---

Memcached is a high-performance, distributed memory object caching system, generic in nature, but originally intended for use in speeding up dynamic web applications by alleviating database load.

Setting up Memcached in ruby on rails application is pretty easy using [dalli][1] gem. Once you install the gem. Configure few settings ie.

 [1]: https://github.com/mperham/dalli

##In gemfile:

{% highlight ruby %}

gem 'dalli'

{% endhighlight %}

<!--more-->


##In config/environments/production.rb:

{% highlight ruby %}

config.cache_store = :dalli_store

{% endhighlight %}

##Installing Memcached

{% highlight ruby %}

brew install memcached  #Mac OSX
apt-get install memcached  #ubuntu

{% endhighlight %}

### If You want to make any change, here is the configuration file:

{% highlight ruby %}

vi /etc/memcached.conf

{% endhighlight %}

### To Check version of Memcached installed:

{% highlight ruby %}

memcached -h | head -l

{% endhighlight %}

### Starting and stopping Memcached

#### In MacOSX:

{% highlight ruby %}
/usr/local/bin/memcached/
{% endhighlight %}

#### On Ubuntu:

{% highlight ruby %}
sudo /etc/init.d/memcached restart
{% endhighlight %}

You can optionally install the ‘kgio’ gem to give Dalli a 20-30% performance boost. Now all the action caching and page caching will be Memcached ;)
