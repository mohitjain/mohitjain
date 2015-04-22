---
title: How to Set an Expires Header in Apache
layout: post
comments: true

permalink: /2012/10/how-to-set-an-expires-header-in-apache/
description: How to ebable mod_expires in apache to set expires headers in apache
kewyords: Expiry headers, apache, mod_expires, performance


categories: optimization performance Server
---

Setting an Expires (or Cache-Control) header in Apache will help speed up your website. I’m running Apache 2.x, and define an expires header for all of the site’s static assets (images, stylesheets, and scripts).

In Apache, mod_expires is a module that allows you to set a given period of time to live for web pages and other objects served from web pages. The idea is to inform web browsers how often they should reload objects from the server. This will save you bandwidth and server load, because clients who follow the header will reload objects less frequently.

##Command to enable mod_expires:

{% highlight ruby %}
a2enmod expires
{% endhighlight %}

##To set an expires header, simply add the following to the “virtualHost” section of your Apache vhost configuration:

{% highlight ruby %}

ExpiresActive On
ExpiresByType image/gif "access plus 1 months"
ExpiresByType image/jpg "access plus 1 months"
ExpiresByType image/jpeg "access plus 1 months"
ExpiresByType image/png "access plus 1 months"
ExpiresByType image/vnd.microsoft.icon "access plus 1 months"
ExpiresByType image/x-icon "access plus 1 months"
ExpiresByType image/ico "access plus 1 months"
ExpiresByType application/javascript “now plus 1 months”
ExpiresByType application/x-javascript “now plus 1 months”
ExpiresByType text/javascript “now plus 1 months”
ExpiresByType text/css “now plus 1 months”
ExpiresDefault "access plus 1 days"

{% endhighlight %}

Alternatively you can add it to your htaccess file in an block.

Also you should enable mod_defalate which will gzip your html, css, and javascript

##Command to enable mod_defalate:

{% highlight ruby %}
a2enmod deflate
{% endhighlight %}
And add these lines:

{% highlight ruby %}
# gzip html, css and js
AddOutputFilterByType DEFLATE text/html text/css application/x-javascript application/javascript
{% endhighlight %}
