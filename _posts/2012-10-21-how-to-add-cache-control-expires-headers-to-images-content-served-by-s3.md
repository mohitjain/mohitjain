---
title: How to add cache-control, expires headers to images (Content) served by S3
layout: post
comments: true



permalink:  /2012/10/how-to-add-cache-control-expires-headers-to-images-content-served-by-s3/
description: How to add cache-control, expires headers to images (Content) served by S3
keywords: amazon s3, paperclip, caching, expiry-headers, images
categories: optimization performance ruby-on-rails
---

Few days back I made a blog post [Save image as progressive image using paperclip and imageMagick][1]. Here is an another improvement in that list.

 [1]: http://www.codebeerstartups.com/save-image-as-progressive-image-using-paperclip-and-imagemagick/

Adding cache control and expiry headers. Caching images improves the user experience and reduces S3 costs. It improves the user’s experience because web pages load quicker as images are already cached and it reduces S3 costs since you have fewer transfers.

From the previous blog post:

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
##Another improvement:
{% highlight ruby %}
has_attached_file :attachment, {
  :styles => {
    :medium => ["654x500>", :jpg],
    :thumb =>["200x200#", :jpg]
  },
  :convert_options => {
    :medium => "-quality 80 -interlace Plane",
    :thumb => "-quality 80 -interlace Plane"
  },
  :s3_headers => { 'Cache-Control' => 'max-age=315576000', 'Expires' => 10.years.from_now.httpdate }
  }.merge(PAPERCLIP_STORAGE_OPTIONS)
{% endhighlight %}

PS: <em>Make sure you reprocess all the attachments :)</em>
