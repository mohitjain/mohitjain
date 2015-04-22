---
layout: post
title: "How to change git commit messages"
description: How to change git commit messages on github
date: 2013-04-09 23:37
categories: git
---


Sometimes I forgot to specify all the details of a commit and it irritates me a lot. Today I just learned a new thing about changing the git commit messages. Its pretty simple. Just run this following command in case you want to change the commit message of the last commit and it will replace the previous message.

{% highlight ruby %}

git commit --amend -m "your new message"

{% endhighlight %}

Pretty simple and nice tip ;)



