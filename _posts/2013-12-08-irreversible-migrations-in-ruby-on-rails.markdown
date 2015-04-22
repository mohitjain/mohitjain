---
title: "Irreversible Migrations in Ruby on Rails "
layout: post
date: 2013-12-08 23:55:53 +0530
permalink: /2012/10/rails-irreversible-migrations/
description: How to make sure migration is Irreversible in ruby on rails
keywords:  optimizations, Irreversible Migrations
categories: migrations ruby-on-rails
---


In Rails 2 in migrations there were only 2 methods: up and down. They are called on running migrations up and down respectively with rake tasks rake db:migrate and rake db:rollback.

Rails 3 produced us great method change which allowed us to write there code which creates a table and drops the table automatically on rolling migration back. But unfortunately there was a problem - you didn't have opportunity to say "don't run this peace of code on down but run this only on up". So the solution was just to use old syntax. Since Rails 4 has released there is a feature to fix this situation.

<!--more-->

##In Rails 2

{% highlight ruby %}
def up
  add_column :users, :active, :boolean
  User.update_all(active: true)
end

def down
  remove_column :users, :active
end
{% endhighlight %}

##In Rails 3

{% highlight ruby %}
def change
  add_column :users, :active, :boolean
end
{% endhighlight %}

##In Rails 4

Rails 4 provides us one more useful way to write what we need in one place:

{% highlight ruby %}
def change
  add_column :users, :active, :boolean
  reversible do |direction|
    direction.up { User.update_all(active: true) }
  end
end
{% endhighlight %}


Checkout the official [documentation](http://api.rubyonrails.org/classes/ActiveRecord/Migration.html#method-i-reversible)
