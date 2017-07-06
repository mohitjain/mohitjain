---
layout: post
title: "How to use git flow in your projects"
date: 2013-04-05 16:05
categories: git git-flow
banner_image: "/wp-content/images/How to use git flow.png"
feature: true
---

Git is a version management tool and I am a big fan of it. I am hoping you came here for git flow. So you have basics of git in your hands. Again on the same note of good practices, I think everyone should work on different branches and then keep merging those branches to the main branch. But that becomes messy cause generally we forget to create a branch. So here is a tool for you.

Note: I am talking about default branches here. You can change that naming convention but I will suggest not to.

So coming back to the topic of git flow.

<!--more-->

#Installation

##Installing on Mac OS X

{% highlight ruby %}

brew install git-flow

{% endhighlight %}

##Installing on Ubuntu

{% highlight ruby %}
apt-get install git-flow
{% endhighlight %}

##Initiating Git flow:

{% highlight ruby %}

git flow init

{% endhighlight %}

It will prompt you something like this:

{% highlight ruby %}

Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []

{% endhighlight %}

Keep pressing enter key to use the defaults. or just do

{% highlight ruby %}

git flow init -d

{% endhighlight %}

for accepting all the defaults.

##Whats the whole process:

* First I want to be on a development branch and keep working on the various tasks of the projects.
* For every task of the project we need to create a branch and then merge that branch into develop branch.
* Once code is production ready. We need to create a release and test the code and make appropriate fixes.
* Merge the fixed code into development branch and into production branch.
* Deploy the code and start working on new tasks of the projects.
* Meanwhile there may be a bug on the production server. We need to fix the code via hotfix and then merge the fixed code on the development branch and production branch.
* Now move back on the task we were actually doing before the hotfix. ;)

So now we have git flow ready in our git repository. Let's do things one by one.

##Create a new feature branch:

For every task we are doing, we will create a feature using git flow. Let's assume we want to implement login task.

{% highlight ruby %}

git flow feature start login

{% endhighlight %}

It will create a new branch with feature namespace is feature/login

Now work on this branch and keep committing your code. Now once done. You want to merge it to develop branch. Here is the command for the same.

{% highlight ruby %}

git flow feature finish login

{% endhighlight %}

It will merge feature/login branch to develop branch and delete this feature/login branch.

Keep creating a new feature branch. Keep working on it. Once done, finish that feature and it will be merged on develop branch. Push that develop branch so that other people can pull it.

{% highlight ruby %}
git push origin develop
git pull origin develop
{% endhighlight %}

##Pushing / pulling a feature.

There may be cases when you need to push feature without merging it develop branch do that this by

{% highlight ruby %}

git flow feature publish name_of_the_feature_like_we_had_login

{% endhighlight %}

if you want to pull any feature

{% highlight ruby %}

git flow feature pull origin name_of_the_feature_like_we_had_login

{% endhighlight %}

##Create a release and push the code to master branch
** ( by default master branch is treated as production branch) **

Now we have code enough coding. We want to finally test the code and then need to push it on production branch. Let's create a release first so that we can test out the once and make appropriate changes if required.

{% highlight ruby %}

git flow release start version_1

{% endhighlight %}

Now test the code and make any changes that you need to make. Commit those changes. Once done.

{% highlight ruby %}

git flow release finish version_1

{% endhighlight %}

This will merge the code into develop branch + master branch and now we can deploy the code from the master branch and then come back to develop branch to implement new tasks.


## Hot fixes

Now we are working on a new cool task and we are on a feature ie my_awesome_task and meanwhile, we came to know that there is a bug in the production on the title of the page. Now we need to do a hotfix.

{% highlight ruby %}

git flow hotfix start typo_bug_in_title

{% endhighlight %}

Now we will fix that title issue and then commit the code and then finish this hotfix.

{% highlight ruby %}

git flow hotfix finish typo_bug_in_title

{% endhighlight %}

This will merge the code into the master branch and into develop branch too. Now you can deploy the code using the master branch and come back to your feature my_awesome_task and do the task. You can check out to your feature branch that you want working on by

{% highlight ruby %}

git flow feature check out my_awesome_task

{% endhighlight %}

I hope this makes some sense. Let me know if you have any doubts or anything.
