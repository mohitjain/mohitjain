---
layout: post
title: "How to find empty columns in your database"
description: How to find empty columns in your database.
keywords: database performance, emplty columns
date: 2013-04-10 00:14
categories: mysql database
---

I need a script to find out empty columns in my application which has a pretty massive database. Here is that small ruby script which helped to get a list of all the columns in the respective table which are null.

Here is a small snippet for the same.


## Snippet

{% highlight ruby %}

  require 'rubygems'
  require 'active_record'

  def query table, column
    "select #{table}.#{column.name} from #{table} where #{table}.#{column.name} is not null or #{table}.#{column.name} != '' limit 1"
  end

  ActiveRecord::Base.establish_connection(
    adapter: 'mysql2',
    database: 'my_sample_database',
    host: 'localhost',
    username: 'username',
    password: 'password',
    pool: 5
  )

  connection = ActiveRecord::Base.connection

  connection.tables.each do |table|
    connection.columns(table).each do |column|
      next if column.name == 'id'

      if ActiveRecord::Base.connection.execute(query table, column).to_a.empty?
        puts "#{table} | #{column.name}"
      end
    end
  end

{% endhighlight %}

Let me know how you want to use this basics scripts.
