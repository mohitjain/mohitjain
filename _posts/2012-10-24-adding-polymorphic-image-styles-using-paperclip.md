---
title: Adding polymorphic image styles using paperclip
author: Mohit Jain
layout: post
comments: true
permalink: /2012/10/adding-polymorphic-image-styles-using-paperclip/
categories: optimization tips-and-tricks
---
Paperclip is one my favorite gem which makes life so easy to upload and process images. Within an application we have a lot of model having images like Product has many pictures, User has many pictures. Now think about a situation where thumb style for the product has size 300> and User model need a size for the thumb is 200>. Here is a quick tip if you want to style the images based on the model.

##Before

{% highlight ruby %}
class Image < ActiveRecord::Base
   belongs_to :imageable, :polymorphic => true
   has_attached_file :attachment, :styles => { :medium => "300>", :thumb => "200>" }
end
{% endhighlight %}

Now we need to modify this model to support polymorphic and styles based on the model. Here is the new code.

{% highlight ruby %}
class Image < ActiveRecord::Base
  belongs_to :imageable, :polymorphic => true
  has_attached_file :attachment, styles: lambda {
    |attachment| {
      thumb: (
        attachment.instance.imageable_type.eql?("Product")? ["300>", 'jpg'] :  ["200>", 'jpg']
      ),
      medium: (
       ["500>", 'jpg']
      )
    }
  }
end
{% endhighlight %}
So this piece of small code will resize you images based upon the model it belongs to. If that image belongs to product then “thumb” will be resize in the format of 300>, else it will be 200. Medium style will be always 500> i.e. independent of model it belongs to. Pretty nice and simple.

Now from previous learning of image optimization i.e. [How to add cache-control, expires headers to images (Content) served by S3][1] and [Save image as the progressive image using paperclip and imageMagick][2], here is the final piece of code.


 [1]: http://www.codebeerstartups.com/how-to-add-cache-control-expires-headers-to-images-content-served-by-s3/
 [2]: http://www.codebeerstartups.com/save-image-as-progressive-image-using-paperclip-and-imagemagick/

{% highlight ruby %}
class Image < ActiveRecord::Base
belongs_to :imageable, :polymorphic => true
has_attached_file :attachment, styles: lambda {
    |attachment| {
      thumb: (
        attachment.instance.imageable_type.eql?("Product")? ["300>", 'jpg'] :  ["200>", 'jpg']
      ),
      medium: (
       ["500>", 'jpg']
      )
    }
  },
  :convert_options => {
    :medium => "-quality 80 -interlace Plane",
    :thumb => "-quality 80 -interlace Plane"
  },
  :s3_headers => { 'Cache-Control' => 'max-age=315576000', 'Expires' => 10.years.from_now.httpdate }.merge(PAPERCLIP_STORAGE_OPTIONS)
end
{% endhighlight %}
