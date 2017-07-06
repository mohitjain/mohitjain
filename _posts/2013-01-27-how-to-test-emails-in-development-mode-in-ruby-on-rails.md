---
title: How to test emails in development mode in ruby on rails
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/how-to-test-emails-in-development-mode-in-ruby-on-rails/
categories: quick-solution tips-and-tricks utilities
---

Testing emails was always a pain for me and my designer friend. my designer friend keeps asking me how can I test emails in development mode in ruby on rails without integrating sendgrid or critsend, so this post dedicated to him only.
I was always looking for a solution for the same, Especially after working on [emaillist.io][1] (A group emailing service.) and today, I got one. [MailCatcher][2].

 [1]: http://emaillist.io/?utm_source=codebeerstartups&utm_medium=blogpost&utm_campaign=codebeerstartups
 [2]: http://mailcatcher.me/

Pretty easy to use and configure. Add in the gem file, add some code in config/development.rb and start the mail catcher daemon. Let's do it one by one.

Add this in your gem file.
<!--more-->

{% highlight ruby %}

gem 'mailcatcher'

{% endhighlight %}

Run bundler and in your development configuration file config/development.rb, set the following Action Mailer settings:

{% highlight ruby %}

config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = { address: 'localhost', port: 1025 }

{% endhighlight %}

and start your rails app and mail catcher daemon from terminal just by typing mail catcher

{% highlight ruby %}

mailcatcher
Starting MailCatcher
==> smtp://127.0.0.1:1025
==> http://127.0.0.1:1080
*** MailCatcher runs as a daemon by default. Go to the web interface to quit.

{% endhighlight %}

Now open http://127.0.0.1:1080 in your browser and you can see a virtual inbox. Try triggering some email from your application and you will email coming in your virtual inbox.
Another awesome feature of MailCatcher is that you can view both the HTML and plain text versions of emails, download attachments and also run some analysis of your email. I just loved it. I hope you will too. ;)

**Make sure before going to production you test it in real scenario’s.**
**
Sample Output**

![How to test emails in development mode in ruby on rails and run tests for various devices like iphone, ipad, blackberry etc.](/wp-content/uploads/2013/01/How-to-test-emails-in-development-mode-in-ruby-on-rails.png?fit=1266,669)
