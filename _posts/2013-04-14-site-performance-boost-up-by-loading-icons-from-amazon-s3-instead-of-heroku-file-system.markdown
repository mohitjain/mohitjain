---
layout: post
title: "Site performance boost up by loading icons from amazon s3 instead of heroku file system"
date: 2013-04-14 18:55
keywords: assets_sync, Amazon s3, Icons, background images, performance, loading icons from amazon s3
categories: preformance,  heroku
---


Loading icons from Heroku file system or Linode or any other hosting will slow down the website. So here are two methods by which you can fix this issue.


##Solution 1:


Move all the background images into image_tag. My designer friend explained me sometimes it's not possible to do that. So here is the second solution.

<!--more-->

##Solution 2:

1. .css should be replaced with .css.scss i.e. saas.
2. Integerate gem for saas  in assets i.e.

{% highlight ruby %}

gem 'sass-rails',   '~> 3.2.3'

{% endhighlight %}
3. Now instead of using

{% highlight css %}

background: #f9f9f9 url('/assets/billie.png');

{% endhighlight %}

Use

{% highlight css %}

background: #f9f9f9 image_url('assets/billie.png');

{% endhighlight %}

Once you do this and have assets hosts specified in the environment file

{% highlight ruby %}

config.action_controller.asset_host = "//#{ENV['FOG_DIRECTORY']}.s3.amazonaws.com"

{% endhighlight %}

All the assets in style sheet will come from Amazon S3.


##How to test solution 2 on local machine:

<!--more-->

1. Specify this in development.rb environment file:

{% highlight ruby %}

config.action_controller.asset_host = "http://localhost:3000"

{% endhighlight %}

2. Make all the changes as specified in step 3 on solution 2 above.
3. Restart the server and load your page having background images. You will see things like:

{% highlight html %}

<link href="http://localhost:3000/assets/application.css?body=1" media="all" rel="stylesheet" type="text/css" />
<link href="http://localhost:3000/assets/token-input-facebook.css?body=1" media="all" rel="stylesheet" type="text/css" />
<link href="http://localhost:3000/assets/token-input.css?body=1" media="all" rel="stylesheet" type="text/css" />
<script src="http://localhost:3000/assets/jquery.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/jquery_ujs.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/jquery-ui.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/jquery.iframe-transport.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/jquery.remotipart.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/autosize.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/hoverscroll.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/rails.validations.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/rails.validations.simple_form.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/tiptip.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/jquery.tokeninput.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/easing.js?body=1" type="text/javascript"></script>
<script src="http://localhost:3000/assets/application.js?body=1" type="text/javascript"></script>

{% endhighlight %}

for your style sheet icons:

{% highlight css %}

.body {
  width: 100%;
  background: #f9f9f9 url(http://localhost:3000/assets/assets/billie.png);
  min-height: 600px;
  overflow: hidden;
  margin-top: 33px;
}

{% endhighlight %}

Previously it was

{% highlight css %}

.body {
  width: 100%;
  background: #f9f9f9 url("/assets/billie.png");
  min-height: 600px;
  overflow: hidden;
  margin-top: 33px;
}

{% endhighlight %}

I hope this makes some sense. For reference how to upload assets on Amazon S3 please check [How to Deploy Assets on Amazon S3 and Why Deploying Assets to Amazon S3 Is Important](http://www.codebeerstartups.com/2012/10/how-to-deploy-assets-on-amazon-s3-and-why-deploying-assets-to-amazon-s3-is-important/):
