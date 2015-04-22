---
title: Configure time zones for your debian based server
author: Mohit Jain
layout: post
permalink: /2012/11/configure-time-zones-for-your-debian-based-server/

categories:  Server
---

Rails always stores your dates in UTC in the database (unless you change a different setting). You can configure time zones for your debian based server just by running this command:

{% highlight ruby %}

sudo dpkg-reconfigure tzdata
# for India, select Asia and then select Kolkata

{% endhighlight %}
