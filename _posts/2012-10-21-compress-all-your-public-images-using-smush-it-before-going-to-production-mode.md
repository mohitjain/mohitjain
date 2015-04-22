---
title: Compress all your public images using smush it, before going to production mode
author: Mohit Jain
layout: post



permalink:  /2012/10/compress-all-your-public-images-using-smush-it-before-going-to-production-mode/
description: How to compress bulk images with ruby on rails
keywords:  performance, compress images, optimize images
categories: General optimization performance quick-solution tips-and-tricks
---

##Compress all your images before going for production mode.

There are lot of services which helps you to optimise your images. But using them is pain in ass. First you have to upload them and then you have to rename them etc. Here is a quick solution. [Smusher][1] a gem for it :)

 [1]: https://github.com/grosser/smusher

{% highlight ruby %}
sudo gem install smusher
{% endhighlight %}
Once you have gem installed. Now a simple command to compress all your assets ;)

{% highlight ruby %}
smusher my_awesome_project/app/assets/images
{% endhighlight %}
This will reprocess all the images in that directory using Yahoo Smushit service and then you are good to go :).

PS: <em>There are some options you can pass while compressing the images. For that checkout the documentation of the gem, pretty nice and clear docs :).</em>
