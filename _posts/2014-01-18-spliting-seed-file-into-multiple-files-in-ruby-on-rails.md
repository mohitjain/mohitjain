---
title: "Spliting Seed files into multiple file in Ruby on Rails"
layout: post
comments: true
date: 2014-01-18 23:55:53 +0530
permalink: /2014/01/spliting-seed-file-into-multiple-files-in-ruby-on-rails/
description: How to manage long seed file of your project. How you can split them into multiple files
keywords:  optimizations, cleanup, seed file, split seed file
categories: ruby-on-rails
---

Last month I joined a new job after a break of almost 4 months. You can check out the [product](http://www.splashmath.com?utm_source=codebeerstartups) and there we had a small problem that our seed file was growing very fast. So we did a small thing to maintain our seed file. Here is a small tip if you are having a massive seed file and it's pretty easy to implement.



We can store all our seeds inside the folder db/seeds and inside the db/seeds.rb we write the following:

{% highlight ruby %}
    Dir[File.join(Rails.root, 'db', 'seeds', '*.rb')].sort.each { |seed| load seed }
{% endhighlight %}
We can sort the files alphabetically before loading them.


## What if seed file ordering is important?

In that case, we can use the trick migrations are using. Timestamp in front of file names to make sure there ordering is same. So instead of using a timestamp, you can add a serial number in front of file name like 01_grades.rb, 02_topics.rb, 03_skills.rb.


I hope this will help someone in case you are facing same issues.
