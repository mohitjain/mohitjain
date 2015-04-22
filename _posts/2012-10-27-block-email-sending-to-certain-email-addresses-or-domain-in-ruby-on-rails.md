---
title: Block email sending to certain email addresses or domain in ruby on rails?
author: Mohit Jain
layout: post
permalink:  /2012/10/block-email-sending-to-certain-email-addresses-or-domain-in-Ruby on Rails/



categories: tips-and-tricks
---

If you want to block email sending to some particular user or some particular email format, then interceptor is your friend :) Just place this code in your config/initializers/email_filters.rb

{% highlight ruby %}

class EmailAddressFilter
  def self.delivering_email(message)
    message.perform_deliveries = false

    # your checks here; return if @abc.com, etc.. is matched
    return unless message.to.join("").match(/@abc.com/).nil?

    # otherwise, the email should be sent
    message.perform_deliveries = true
  end
end

ActionMailer::Base.register_interceptor(EmailAddressFilter)

{% endhighlight %}

All of your emails will be blocked matching that regex :)
