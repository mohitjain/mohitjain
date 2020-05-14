---
title: Rollback all database changes on exit
author: Mohit Jain
layout: post
comments: true
categories: General quick-solution tips-and-tricks utilities
---
Being a Rails developer, Lot of time I spend on rails console. Ever thought of rollback all changes you have done on console? Yes? Here is a quick tip for you ;)


{% highlight ruby %}

  rails c --sandbox
  Loading development environment in sandbox.
  Any modifications you make will be rolled back on exit.
  >>

{% endhighlight %}

You can also use -s as a flag instead of –sandbox. Awesome!
