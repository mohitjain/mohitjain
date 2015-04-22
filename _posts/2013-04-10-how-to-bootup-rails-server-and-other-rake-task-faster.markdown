---
layout: post
title: "How to bootup rails server and other rake task faster"
description: Rails server loads pretty slow? Rake db:migrate and scaffolding takes too much time?
keywords: Ruby on rails, load time, server starts too slow, run test case faster
date: 2013-04-10 22:23
categories: development tips-and-tricks
---


Most frustating moments while developing apps with rails is server bootup time. Running rake db:migrate takes likes year and other generates like scaffold and running custom rake tasks takes too much time to start. All because it loads the whole environment and then do the stuff and few days back came to know to about an awesome gem ie [zeus](https://github.com/burke/zeus), which keep the rails environment loaded and your generators lesser time that you can even observe. You can find a [railscasts](http://railscasts.com/episodes/412-fast-rails-commands) for the same. Still here is the small description.

<!--more-->

##Installation

Don't install via bundler.

{% highlight ruby %}

gem install zeus

{% endhighlight %}

##Usage

Start the zeus server ie

{% highlight ruby %}

zeus start

{% endhighlight %}

Now run your various commands like

{% highlight ruby %}

zeus g model comment content
zeus rake db:migrate
zeus rake test
zeus test test/functional
zeus rake db:migrate

{% endhighlight %}

Trust me just try out once. Its like your machine is a super computer now. There are few more solutions out there. You can check railscasts for the same as specified earlier.
