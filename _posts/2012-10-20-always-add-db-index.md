---
title: Always add DB index
layout: post
comments: true
comments: true
description: How to add database index in ruby on rails to optimize your database performance
keywords: performance, mysql, index,  optimizations, query optimizations
categories: Performance ruby-on-rails
---

Always add DB index for foreign key, columns that need to be sorted, lookup fields and columns that are used in a GROUP BY. This can improve the performance of SQL query.

##Bad Smell

{% highlight ruby %}
class CreateComments < ActiveRecord::Migration
   def self.up
      create_table "comments" do |t|
        t.string :content
        t.integer :post_id
        t.integer :user_id
      end
   end

   def self.down
       drop_table "comments"
   end
end
{% endhighlight %}

By default, Rails does not add indexes automatically for foreign key, you should add indexes by yourself.

##Refactor

{% highlight ruby %}
class CreateComments < ActiveRecord::Migration
   def self.up
      create_table "comments" do |t|
          t.string :content
          t.integer :post_id
          t.integer :user_id
      end

      add_index :comments, :post_id
      add_index :comments, :user_id
  end

  def self.down
    drop_table "comments"
  end
end
{% endhighlight %}

This is a basic practice, follow it.
