---
layout: post
title: "How to pull push from multiple git repositories"
description: How to pull and push from multiple github repositories.
keywords: git, github, multple origins, multiple git repositories
date: 2013-04-09 22:56
categories: git
---

A lot of time I have seen people asking how to handle two git repo from the same directory. It seems pretty simple as most of them have pushed much application on Heroku. So on regular basis, they keep pushing code to GitHub or Bitbucket and once everything is tested out, they push their code on Heroku. Which is exactly what they are asking.

Ok, enough with the stories, it's all about setting a new different origin. Let me explain this via Heroku example. When you are using Github, to push the code on master branch you do it via

<!--more-->

{% highlight ruby %}

git push origin master

{% endhighlight %}

Now to push it on Heroku, you do

{% highlight ruby %}

git push heroku master

{% endhighlight %}

Here you are doing the same, pushing the code to different repositories where things are different from two origin points ie Heroku and origin :).

So let's assume we have two repositories ie repository_1 and repository_2 with remote URLs  git@github.com:mohitjain/repository_1.git and git@github.com:mohitjain/repository_2.git respectively.

Now setup two different origins in your local git repository

{% highlight ruby %}

git remote add origin_1 git@github.com:mohitjain/repository_1.git
git remote add origin_2 git@github.com:mohitjain/repository_2.git

{% endhighlight %}

Now you can push on repository_1 by:

{% highlight ruby %}

git push origin_1 master

{% endhighlight %}

and in another repository_2 by:

{% highlight ruby %}
    git push origin_2 master
{% endhighlight %}
Similarly, you can pull from different repositories.

Or create aliases something like this (Be careful while doing this):

{% highlight ruby %}
alias pushall='for i in `git remote`; do git push $i; done;'
alias pullall='for i in `git remote`; do git pull $i; done;'
{% endhighlight %}
