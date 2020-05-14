---
title: Save image as progressive image using paperclip and imageMagick
author: Mohit Jain
layout: post
comments: true
keywords: image optimaztions,  image magick, paperclip, progressive image, performance, optimizations
categories: optimization performance ruby-on-rails
---
We all have upload image functionality in our web apps. But we people don’t optimize the images uploaded by the user.

Here are the two quick things you can do to optimize your images:

1.  Reduce the quality of the pictures. You need to take the call, How much?
2.  Save images as progressive pictures.

# How to do save image as progressive image using paperclip:

## Before:

{% highlight ruby %}

    has_attached_file :attachment, {
      :styles => {
        :medium => ["654x500>", :jpg],
        :thumb =>["200x200#", :jpg]
      }

{% endhighlight %}

## After:

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
    }
{% endhighlight %}

## -quality 80 -interlace Plane
 is the code which do all the magic behind the screens. 80 is the factor of reducing image quality and interlace plane saves the image as progressive image :)

Let the more suggestions come for image optimizations.
