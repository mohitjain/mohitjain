---
layout: post
title: Lazy Loading of Images in Rails
author: Mohit Jain
comments: true
categories: Image optimizations, lazy-loading
description: How to lazy load images in ruby on rails.
---

I recently came across a lot of lazy loading javascript plugins, but finally came to know about [Layzr plugin](https://github.com/callmecavs/layzr.js) simple, lightweight and works like charm.

But the problem is the usage. So what we use in rails:

{% highlight ruby %}
  <%= image_tag "my_image.jpg" %>
{% endhighlight %}

which generates an HTML code like this:

{% highlight ruby %}
  <img src="my_image.jpg"/>
{% endhighlight %}

Now layzr javascript plugin is expecting something like this:

{% highlight ruby %}
  <img data-normal="my_image.jpg"/>
{% endhighlight %}

and later on, it gets converted into using javascript:

{% highlight ruby %}
  <img scr="my_image.jpg"/>
{% endhighlight %}

So what I want is a default image which will be loaded when page load happens and while scrolling default image should be replaced by a real image. So I can do it something like:

{% highlight ruby %}
  <%= image_tag "default_image.jpg", "data-normal" => "my_real_image.jpg" %>
{% endhighlight %}

or while using the paperclip as a gem makes it like:

{% highlight ruby %}
  <%= image_tag "default_image.jpg", "data-normal" => image.photo.url(:medium) %>
{% endhighlight %}

The above code is ugly. I don't want to screw up my whole image_tag, so wrote a simple ruby gem to write a clean code, which takes a default image from configuration files and do the magic behind the screen. ie:

{% highlight ruby %}
  <%= image_tag "my_real_image.jpg", lazy: true %>
{% endhighlight %}

This gets converted into:

{% highlight ruby %}
  <img src="default_image.jpg" data-normal="my_image.jpg"/>
{% endhighlight %}

## How to use it:

All you need to do is:

### Step 1:

Add it in your Gemfile

{% highlight ruby %}
  gem 'layzr-rails'
{% endhighlight %}

### Step 2:

Create a configuration file and put it in your initializers config/initializers/layzr.rb

{% highlight ruby %}
  Layzr::Rails.configure do |config|
    config.placeholder = "/assets/some-default-image.png"
  end
{% endhighlight %}

### Step 3:

Download layzr.js and include in application js and place this code:

{% highlight ruby %}
  $(document).ready(function() {
     const instance = Layzr()
  });
{% endhighlight %}

### Step 4:

Images you want to make lazy load:

{% highlight ruby %}
  <%= image_tag "kittenz.png", alt: "OMG a cat!", lazy: true %>
{% endhighlight %}

### That's all :)

that makes my code clean and efficient. You can use see the source code [here](https://github.com/mohitjain/layzr-rails) having guidelines how to use it and some more options from the gem.
