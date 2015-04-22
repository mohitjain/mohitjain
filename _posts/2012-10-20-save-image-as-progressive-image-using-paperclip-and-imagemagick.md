---
title: Save image as progressive image using paperclip and imageMagick
author: Mohit Jain
layout: post
comments: true

permalink: /2012/10/save-image-as-progressive-image-using-paperclip-and-imagemagick/
keywords: How to reduce the size of image. How to save images as progressive image using paperclip and imagemagick in ruby on rails.


keywords: image optimaztions,  image magick, paperclip, progressive image, performance, optimizations
categories: optimization performance ruby-on-rails
---

We all have upload image functionality in our web apps. But we generally people don’t optimise the images uploaded by user.

Here are the two quick things you can do to optimise your images:

1.  Reduce the quality of the images. You need to take the call, How much?
2.  Save images as progressive images.

##How to do save image as progressive image using paperclip:

##Before:

{% highlight ruby %}
has_attached_file :attachment, {
    :styles => {
      :medium => ["654x500>", :jpg],
      :thumb =>["200x200#", :jpg]
    }
{% endhighlight %}
##After:

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
##-quality 80 -interlace Plane
 is the code which do all the magic behind the screens. 80 is the factor of reducing image quality and interlace plane saves the image as progressive image :)

Let the more suggestions come for image optimizations…!!!
