---
title: Not able to start rails application as port 3000 is already in use.
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/not-able-to-start-rails-application-as-port-3000-is-already-in-use/



categories:  Server tips-and-tricks utilities
---

I have faced this issue so many times, may be because I accidentally closed the terminal or something else. Because of that my 3000 or some other port is blocked, and I am not able to start the application on the same port. In that case you will get an error like this:

{% highlight ruby %}

.rvm/gems/ruby-1.9.3-p194/gems/eventmachine-1.0.0/lib/eventmachine.rb:526:in `start_tcp_server': no acceptor (port is in use or requires root privileges) (RuntimeError)
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/eventmachine-1.0.0/lib/eventmachine.rb:526:in `start_server'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/thin-1.5.0/lib/thin/backends/tcp_server.rb:16:in `connect'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/thin-1.5.0/lib/thin/backends/base.rb:55:in `block in start'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/eventmachine-1.0.0/lib/eventmachine.rb:187:in `call'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/eventmachine-1.0.0/lib/eventmachine.rb:187:in `run_machine'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/eventmachine-1.0.0/lib/eventmachine.rb:187:in `run'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/thin-1.5.0/lib/thin/backends/base.rb:63:in `start'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/thin-1.5.0/lib/thin/server.rb:159:in `start'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/rack-1.4.1/lib/rack/handler/thin.rb:13:in `run'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/rack-1.4.1/lib/rack/server.rb:265:in `start'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/railties-3.2.8/lib/rails/commands/server.rb:70:in `start'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/railties-3.2.8/lib/rails/commands.rb:55:in `block in '
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/railties-3.2.8/lib/rails/commands.rb:50:in `tap'
	from /Users/*me*/.rvm/gems/ruby-1.9.3-p194/gems/railties-3.2.8/lib/rails/commands.rb:50:in `'
	from script/rails:6:in `require'
	from script/rails:6:in `'

{% endhighlight %}

A solution to this problem is **Restart your machine**, (*Kidding*):

{% highlight ruby %}
lsof -i :3000
{% endhighlight %}
In port 3000 is already in use, else replace 3000 with your port number like 4000 etc.
This will result out the PID and then you can kill the process in order to make your port free :)
{% highlight ruby %}
kill -9 PID
{% endhighlight %}
Now your port is released and you can start your application on the same port.
