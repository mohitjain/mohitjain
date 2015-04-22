---
layout: post
title: "Use belongs_to with presence validator"
description: How to validate belongs_to object exists in the database
date: 2013-07-13 22:35
categories: validations, associations
keywords: belongs_to, validations, associations
---


Assume we have two models: User and Image. User has one image and image belongs to user. The code below:

{% highlight ruby %}
class User < ActiveRecord::Base
  has_one :image
end

class Image < ActiveRecord::Base
  belongs_to :user
end
{% endhighlight %}

Now we want to add validation for image to check if user is there or not.

<!--more-->

{% highlight ruby %}
class Image < ActiveRecord::Base
  belongs_to :user
  validates :user, :presence => true
end
{% endhighlight %}

So by adding just one line whenever you are trying to save image object, it will fire a query with respect to the user_id to check weather that user exists or not. In case user doesn't exits "image.save" with return an error.


Happy Hacking :)
