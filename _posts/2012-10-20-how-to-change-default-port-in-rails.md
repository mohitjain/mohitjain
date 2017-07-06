---
title: How to change default port in rails
layout: post
comments: true
permalink: /2012/10/how-to-change-default-port-in-rails/
description: How to change default port in ruby on rails
keywords: port, default port, ruby on rails
categories: tips-and-tricks
---

Append these code lines in config/boot.rb:
{% highlight ruby %}
require'rails/commands/server'
module Rails
  class Server
    alias:default_options_alias :default_options
    def default_options
      default_options_alias.merge!(:Port=>3333)
    end
  end
end
{% endhighlight %}
Now default port is 3333 :)
