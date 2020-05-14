---
layout: post
title: "How to generate css sprites automatically using a gem in ruby on rails"
date: 2013-04-04 20:48
categories: Performance
---

CSS sprites is a pretty cool thing to implement but its tedious one as you have to compose a lot of images into one CSS sprite image and measure the x and y positions for each image. Besides this, it always causes conflict when more than one person changes the CSS sprite image. So here is a trick for you. Use a gem ie [css_sprite](https://github.com/flyerhzm/css_sprite) and it will create merge all the images and write down the respective CSS for you.

Something like this:

{% highlight css %}

  .twitter_icon,.facebook_icon,.login_button,.logout_button {
    background: url('/images/css_sprite.png?1270170265')no-repeat;
  }
  .twitter_icon { background-position:0px0px; width:14px; height:14px;}
  .facebook_icon { background-position:0px-19px; width:14px; height:14px;}
  .login_button { background-position:0px-38px; width:103px; height:36px;}
  .logout_button { background-position:0px-79px; width:103px; height:36px;}

{% endhighlight %}




These are CSS sprite best practice I follow. Now it's time to see how to implement these in a Rails application.

* Install the css_sprite gem
* Create css_sprite or css_sprite suffixed directory, and put any images into the CSS sprite directory.
* You can use "rake css_sprite:start" to generate CSS sprite image automatically all the time, or use "rake css_sprite:build" to run the css_sprite once manually.
* Then add the stylesheet "css_sprite.css" in HTML and use the generated CSS class to display image.

The css_sprite gem also supports to generate sass and scss.
And to avoid the conflict of CSS sprite image and CSS, add public/images/css_sprite.png and public/stylesheets/css_sprite.css into .gitignore file. So only images under CSS sprite directory are in the control of git, and everyone should build the CSS sprite image automatically by the rake task.
You can find more details [here](http://huangzhimin.com/2010/04/03/css-sprite-best-practices-english-version/)
