---
layout: post
title: Lazy Loading of Images in Rails
author: Mohit Jain
comments: true
categories: Image optimizations, lazy-loading
---

Recently I joined a company thats [Thrillophilia](http://www.thrillophilia.com/) a tours and activities company in India, and where I need to solve a problem of lazy loading of images, cause the site is image heavy. I came across lot of lazy loading javascript plugins, but finally came to know about [Layzr plugin](https://github.com/callmecavs/layzr.js) simple, lightweight and works like charm. 

<!--more-->

But the problem is the usage. So what we use in rails is:

      <%= image_tag "my_image.jpg" %>

which generates a code like this:

      <img src="my_image.jpg"/>      


Now layzr javascript plugin is expecting something like this:

      <img data-normal="my_image.jpg"/>

and later on it converted into

      <img scr="my_image.jpg"/>

So what I want is a default image which will be loaded when page load happens and while scrolling default image should be replaced by real image. So I can do it something like:

      <%= image_tag "default_image.jpg", "data-normal" => "my_real_image.jpg" %>

or while using paperclip as a gem makes it like:

      <%= image_tag "default_image.jpg", "data-normal" => image.photo.url(:medium) %>      

The above code is ugly. I don't want to screw up my whole image_tag, so wrote a simple ruby gem to write a clean code, which takes a default image from configuration files and do the magic behind the screen. ie:

      <%= image_tag "my_real_image.jpg", lazy: true %>

This gets converted into:

      <img src="default_image.jpg" data-normal="my_image.jpg"/>

## How to use it:      

All you need to do is:

### Step 1:

Add it in your gemfile

    gem 'layzr-rails'

### Step 2:

Create a configuration file and put it in your initializers config/initializers/layzr.rb


    Layzr::Rails.configure do |config|
      config.placeholder = "/assets/some-default-image.png"
    end

### Step 3:

Download layzr.js and include in application js and place this code:

    $(document).ready(function() {
       const instance = Layzr()
    });

### Step 4:

Images you want to make lazy load:

    <%= image_tag "kittenz.png", alt: "OMG a cat!", lazy: true %>


### Thats all :)

thats makes my code clean and efficient. You can use see the source code [here](https://github.com/mohitjain/layzr-rails) having guidelines how to use it and some more options from the gem.




