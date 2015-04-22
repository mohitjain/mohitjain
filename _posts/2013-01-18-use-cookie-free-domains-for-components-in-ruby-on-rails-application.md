---
title: Use cookie-free domains for components in ruby on rails application.
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/use-cookie-free-domains-for-components-in-ruby-on-rails-application/



categories: optimization performance quick-solution Server tips-and-tricks utilities
---

Use cookie-free domains for components in ruby on rails application is important to speed up your website.
If you deliver assets (image, stylesheet and javascript) from the same domain, the server will pass cookies for each asset request, which is not necessary and waste your bandwidth and according to one of the Yahoo’s best practices use cookie-free domains for components for speeding up your web site.

We can do the same thing in ruby on rails by defining a different domain for application and assets, that make your assets load faster.

Create a subdomain for your application and use that subdomain to deliver assets for the application. So once subdomain created and propagated paste this in your production.rb

{% highlight ruby %}
config.action_controller.asset_host ="http://assets.myawesomedomain.com"
{% endhighlight %}
Then create an asset host like this

**Gor Nginx:**

{% highlight ruby %}
server {
    listen 80;
    server_name assets.myawesomedomain.com;
    root /home/deployer/my_rails_app/production/current/public;
}
{% endhighlight %}
**For Apache**

{% highlight ruby %}
ServerName assets.myawesomedomain.com
DocumentRoot /home/deployer/my_rails_app/production/current/public
{% endhighlight %}

Now just restart your server and agin deploy your application. You will see all the assets are loaded from assets.myawesomedomain.com without cookies. Check [GTMetrics][1] ratings for more optimisations.

 [1]: http://gtmetrix.com/
