---
layout: post
title: "How to find the location of the method where its defined"
keywords: Method defination, ruby, method location, ruby metaprogramming
date: 2013-04-14 14:25
categories: ruby
---

A lot of time I got pissed to find where is the method is defined in the case when there are so many modules or when I checking the source code of a gem. Here is a small tip using a very basic example.

For example, You have a method full_name in the user model, now, in this case, you know the location but the question is how you can find the location of the file. Here is the thing. Open rails console and try this:



{% highlight ruby %}

  User.first.method(:full_name).source_location
  ["/Users/mohit/projects/my_awesome_app/app/models/user.rb", 17]

{% endhighlight %}

Or let's assume there is a class method defined in some module, placed somewhere in the lib directory and that module in included in the User model.

{% highlight ruby %}

  User.method(:my_class_method_defined_in_some_module).source_location
  ["/Users/mohit/projects/my_awesome_app/lib/modules/my_awesome_module.rb", 7]

{% endhighlight %}

So source_location is the main thing here and it will work only for Ruby 1.9+. You can read more about it [here in ruby docs](http://www.ruby-doc.org/core-1.9.3/Method.html#method-i-source_location).
