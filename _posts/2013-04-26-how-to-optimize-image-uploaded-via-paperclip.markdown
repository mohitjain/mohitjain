---
layout: post
title: "How to optimize image uploaded via paperclip"
date: 2013-04-26 22:28
description: How to reduce size of images uplaoded via paperclip make your website load faster.
keywords: reduce images size, paperclip, performance
categories: paperclip performance optimizations
---

Previously I wrote a post for [saving image as progessive image](http://www.codebeerstartups.com/2012/10/save-image-as-progressive-image-using-paperclip-and-imagemagick/), continuing the same, here is an another gem to reduce the size of the progressive image.

{% highlight ruby %}

gem "paperclip-compression","~> 0.1.1"

{% endhighlight %}

<!--more-->

##Usage

{% highlight ruby %}

class User < ActiveRecord::Base
		 has_attached_file :avatar,
              :styles     => { :medium => "300x300>", :thumb => "100x100>" },
              :processors => [:thumbnail, :compression]
end

{% endhighlight %}
From [previous learnings](http://www.codebeerstartups.com/2012/10/save-image-as-progressive-image-using-paperclip-and-imagemagick/) we can optimize this code as:

{% highlight ruby %}

has_attached_file :attachment, {
:styles => {
  :medium => ["654x500>", :jpg],
  :thumb =>["200x200#", :jpg]
},
:convert_options => {
  :medium => "-quality 80 -interlace Plane",
  :thumb => "-quality 80 -interlace Plane"
  }
},
 :processors => [:thumbnail, :compression]

{% endhighlight %}
After using this optimization trick I am able to save approx 20% of image size in my projects. Pretty nice and clean.
