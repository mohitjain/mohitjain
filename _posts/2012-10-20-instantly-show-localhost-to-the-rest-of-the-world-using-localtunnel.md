---
title: Instantly show localhost to the rest of the world using localtunnel
author: Mohit Jain
layout: post
comments: true
permalink: /2012/10/instantly-show-localhost-to-the-rest-of-the-world-using-localtunnel/
description: Instantly show localhost to the rest of the world using localtunnel
keywords:  localhost, localmachine as server
categories: quick-solution tips-and-tricks
---

Sometimes you really want to show your local running code to outside world, your friends or colleague. Here is one quick solution.

##STEP 1:
 Install localtunnel using RubyGems.
{% highlight ruby %}
sudo gem install localtunnel
{% endhighlight %}
##STEP 2:
 Run your local web server on any port! Let’s say you’re running WEBrick on port 3000.

##STEP 3:
 Now run localtunnel passing it the port to share.
{% highlight ruby %}
localtunnel 3000
{% endhighlight %}
The first time you run localtunnel you have to point to a public SSH key.
{% highlight ruby %}
localtunnel -k ~/.ssh/id_rsa.pub 3000
{% endhighlight %}
You should see something like this:

Port 3000 is now publicly accessible from abc.localtunnel
