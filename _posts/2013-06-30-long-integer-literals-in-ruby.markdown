---
layout: post
title: "Long integer literals in ruby"
description: How you read number of zeros in a long integer in ruby
date: 2013-06-30 00:49
categories: ruby tips-and-tricks
---

I am here to share a small tip that I just come to know about ruby. A simple question. How many zeros are there integer written below?

{% highlight ruby %}

100000000000

{% endhighlight %}

Difficult to count right? In normal day to day practice we generally use comma to separate the digits, for example in US standard we use comma every 3 digits. So number written above can be re-written as:

{% highlight ruby %}

100,000,000,000

{% endhighlight %}

Now same thing can be done with long integers in ruby using an underscore, something like this:

{% highlight ruby %}

100_000_000_000

{% endhighlight %}

which is actually same as writing 100000000000, but using underscore makes things more easy to read;)

I hope you will find this technique somewhere useful ;)







