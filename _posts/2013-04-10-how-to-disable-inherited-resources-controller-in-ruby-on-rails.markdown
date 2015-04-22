---
layout: post
title: "How to disable inherited_resources controller in ruby on rails"
description: How to disable inherited_resources controller so that 'rails scaffold'  work normally if inherited_resources used by another gem
keywords: active_admin, inherited_resources, rails scaffold
date: 2013-04-10 21:22
categories: Inherited-resources ruby-on-rails
---

I am using active_admin in my projects which use inherited_resources to generate controllers. Now because of my whenever I do scaffolding, generated controller is is inherited_resources controller not the normal generated controller. I found this pretty irritating cause I don't want to use inherited_resources. So I was looking for a solution for the same. Here is a small thing I did. You should be able to do the same in your app, configuring back to the default :scaffold_controller, by adding this to your application.rb file:

<!--more-->

## Solution 1

{% highlight ruby %}

config.app_generators.scaffold_controller = :scaffold_controller

{% endhighlight %}

## Solution 2

{% highlight ruby %}

config.generators do |g|
  g.scaffold_controller "scaffold_controller"
end

{% endhighlight %}

## Solution 3


> To force rails to use the normal scaffold generator, add -c=scaffold_generator to the end of the command


I prefer solution 1 or solution 2. But solution 3 can be helpful in some cases.


