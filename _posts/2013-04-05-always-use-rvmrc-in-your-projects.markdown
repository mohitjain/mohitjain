---
layout: post
title: "Always use rvmrc in your projects"
date: 2013-04-05 13:48
categories: rvm ruby-on-rails
---


I have seen some people who don't use .rvmrc file in their projects which seems to be a very bad approach as things go messy when you need multiple versions of ruby or multiple versions on rails, as some gems versions are dependent on rails version you are using. Its seems too much lazyness as create a .rvmrc file and adding configuration is like 2 mins job.

Ok lets improve our habbit and lets see how we can use .rvmrc file. So any rails project as we add .gitignore file. Same way we need to create a .rvmrc file in the root directory and paste the following content

<!--more-->

{% highlight ruby %}

rvm use 1.9.3@example.com --create

{% endhighlight %}

Replace example.com with your project name and 1.9.3 with the ruby version you want to use. Now leave the directory by cd .. and enter the project directory again. It will prompt you to something like this:

{% highlight ruby %}

********************************************
* NOTICE                                                                                                           *
********************************************
* RVM has encountered a new or modified .rvmrc file in the current directory, this is a shell script and           *
* therefore may contain any shell commands.                                                                        *
*                                                                                                                  *
* Examine the contents of this file carefully to be sure the contents are safe before trusting it!                 *
* Do you wish to trust '/Users/mohit/projects/ninjahr/.rvmrc'?                                                     *
* Choose v[iew] below to view the contents                                                                         *
*********************************************
y[es], n[o], v[iew], c[ancel]>

{% endhighlight %}
Press y and it will create a new gemset for you based upon the name of the project specified in .rvmrc file and force to use ruby version specified.  You need to install all the gems once and then its all up and running.

Use case for this is creating gem sets for all the projects and using specified version of ruby in that project. You all the gem are installed in a group for that project. No more frustation when you update gems of one project and things go messy in another project. ;)

You can find more details on official rvm site [here.](https://rvm.io/workflow/projects/)

