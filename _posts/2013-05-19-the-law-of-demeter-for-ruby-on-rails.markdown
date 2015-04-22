---
layout: post
title: "The Law of Demeter for ruby on rails"
date: 2013-05-19 00:00
categories: performance improvements ruby-on-rails
---

According to the law of demeter, a model should only talk to its immediate association, don't talk to the association's association and association's property, it is a case of loose coupling.


##Bad Smell

{% highlight ruby %}

class Invoice < ActiveRecord::Base
  belongs_to :user
end

<%= @invoice.user.name %>
<%= @invoice.user.address %>
<%= @invoice.user.cellphone %>

{% endhighlight %}

In this example, invoice model calls the association(user)'s property(name, address and cellphone), which violates the law of demeter. We should add some wrapper methods.

<!--more-->

##Refactor

{% highlight ruby %}

class Invoice < ActiveRecord::Base
  belongs_to :user
  delegate :name, :address, :cellphone, :to => :user, :prefix => true
end

<%= @invoice.user_name %>
<%= @invoice.user_address %>
<%= @invoice.user_cellphone %>

{% endhighlight %}

Luckily, rails provides a helper method delegate which utilizes the DSL way to generates the wrapper methods. Besides the loose coupling, delegate also prevents the error call method on nil object if you add option :allow_nil => true.

[Source](http://rails-bestpractices.com/posts/15-the-law-of-demeter)
