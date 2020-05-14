---
title: How to implement action caching in ruby on rails with ajax enabled
author: Mohit Jain
layout: post
comments: true
categories: optimization performance quick-solution tips-and-tricks
---

As a ruby on rails developer, you can implement caching pretty fast. As all, we know there are three kinds of caching

*   Page Caching
*   Action Caching
*   Fragment caching




So here is the major difference in three type of caching and then let's just implement action_caching in just a few lines.

* **Page Caching** -> An HTML page will be saved in your public directory. No before filters etc will be triggered once page is cached
* **Action Caching** ->  It's more or less same like page caching but before_filters will be executed in this case and that's the best part of it.
* **Fragment caching** -> It will be used in the case when you want to cache a specific segment of a page like a sidebar etc.

Ok. Let's move to action caching in Ruby on rails and you can enable caching by setting perform_caching true in development environment

{% highlight ruby %}

  config.action_controller.perform_caching = true

{% endhighlight %}

Lets cache index action of products controller. You can do that by specifying this line in you controller:

{% highlight ruby %}

  caches_action :index

{% endhighlight %}

Pretty easy :)

## Case 1:

You have pagination implemented on this index action and you want to cache different pages. Pretty easy:

{% highlight ruby %}

  caches_action :index, :cache_path => Proc.new { |c| c.params }

{% endhighlight %}

##Case 2:

You have pagination implemented on this index action and you want to cache different pages. But not for logged in user. You want to cache only for logged out users.

{% highlight ruby %}

  caches_action :index, :unless => :current_user, :cache_path => Proc.new { |c| c.params }

{% endhighlight %}

*(I am using devise so current_user method is there. Make sure you have current_user method)*

## Case 3:

You have pagination implemented on this index action and you want to cache different pages. But not for logged in user. You want to cache only for logged out users and you want to expire this cache in every 10 mins.

{% highlight ruby %}

  caches_action :index, :unless => :current_user, :cache_path => Proc.new { |c| c.params },:expires_in => 10.minutes

{% endhighlight %}


## Case 4:

Sometimes we want to reject a specific parameter may some query string parameters, so you can do:

{% highlight ruby %}

  caches_action :index, :unless => :current_user, :cache_path => Proc.new { |c| c.params.except(:reject_this_specific_parameter)},:expires_in => 10.minutes

{% endhighlight %}

## Case 5:

Cache Ajax and HTML request both. Before we check how to do that. Let's talk about Ajax. We all know how to implement ajax requests in Ruby on Rails ie remote => true in the link_to method. But so far I am not able to figure out how to do action caching when it's enabled. So it's a little bit Jack I have posted a question on [stackoverflow][3], but not getting any solution for that. If you know please let me and I will update this post ;)

 [3]: http://stackoverflow.com/q/13635548/179855

So paste this code in your application.js (You may want to bind it to a live event, But I am leaving it up to you.)

{% highlight javascript %}

  $(function(){
    $('.pagination a').click(function(){
      $.ajax({
        url: this.href,
        dataType: 'script'
      });
      return false;
    });
  });

{% endhighlight %}

And in the controller:

{% highlight ruby %}

  caches_action :index, cache_path: proc { |c| c.params.except(:_).merge(format: request.format)}

{% endhighlight %}

So that's all about the action caching in Ruby on rails with params options. Make sure you follow all the rails casts to implement caching in a better way because there are a lot of things you need to take care in case of caching. Also, there are sweepers which can help you to clear cache as per the events instead of just time-based.

One last thing. To clear cache in development mode, you can Rails.cache.clear from the console. :) and also take a look how to [setup Memcached in ruby on rails][4]

 [4]: http://www.codebeerstartups.com/2013/01/quick-way-to-setup-memcached-in-Ruby on Rails-application/ "Quick way to setup Memcached in Ruby on Rails application"


You can read in detail about all of these from [rails guides][1] and there are so many [railscasts there on the same topic ie caching in Ruby on rails][2]

  [1]: http://guides.rubyonrails.org/caching_with_rails.html "Caching in ruby on rails"
  [2]: http://railscasts.com/episodes?search=caching "Caching in ruby on rails"
