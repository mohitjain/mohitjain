---
title: Use say and say_with_time in migrations to make a useful migration log
layout: post
comments: true
permalink: /2012/10/use-say-and-say_with_time-in-migrations-to-make-a-useful-migration-log/
description: How to output migrations logs to understand the migration stuff
keywords: migrations, logs
categories: tips-and-tricks
---

Use say_with_time and say in migrations will produce a more readable output in migrations. And if use correctly it could be a helpful friend when something goes wrong because usually it is stored in the deploy log

Is a good practice to use say_with_time and say in migrations. When doing multiple things in a migration, it is more explanatory than just show the name of the file.

For example, imagine you have a migration that just updates column information for all users.


##Example

{% highlight ruby %}
class UpdateUsersNames < ActiveRecord::Migration
  def self.up
    say_with_time("Spliting name to extract last name")do
      User.find_each do|user|
        user.firstname, user.lastname = name.match(/^([^s]*)s*(.*)$/).to_a[1..-1] if user.changed?
        user.save
        say "#{user.id} was updated"
      end
    end
  end

  def self.down

  end
end
{% endhighlight %}
##Output

{% highlight ruby %}
==  UpdateUserName: migrating =================================================
--Spliting name to extract last name
--859302 was updated
--859303 was updated
   ->0.0786s
==  UpdateUserName: migrated (0.0787s)========================================
{% endhighlight %}
