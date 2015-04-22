---
layout: post
title: "Parallel gem installing using Bundler"
date: 2013-09-02 04:09
description: How to install gems parallely. Bundler is taking too much to install gems.
categories: ruby-on-rails bundler
keywords: bundler, bundler is taking too much time,  bundler is too slow, gems install, install gems faster
---


![My bundler is running](/wp-content/images/bundler.png)


No more waiting time. Bundler supports faster gem install as it [adds support for parallel installation](https://github.com/bundler/bundler/pull/2481). You can pass in --jobs=SIZE (or -jSIZE) as a parameter to bundle install

<!--more-->

##How can I use this now?

Simple! Just install a prerelease version of Bundler, and you should be good to go:

{% highlight ruby %}
    gem install bundler --pre
{% endhighlight %}
So now the problem that bundler is taking too much time is long gone. Happy coding :)
