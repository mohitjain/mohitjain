---
title: Git Happy Commits using git/hooks/post-commit
author: Mohit Jain
layout: post
comments: true
permalink: /2012/11/git-happy-commits-using-git-hooks-post-commit/



categories: Git
---

Giggle every time you make a commit. This is how sound will play after every git happy commits :)

[Sound file it plays:][1]

 [1]: http://www.codebeerstartups.com/wp-content/uploads/2012/11/happykids.wav "Sound it plays"

**How to guide:**

1.  Open you project in terminal.
2.  “ls -a” command will tell you all the hidden directories. If you have git initialised then you will see a .git hidden directory there. If yes then proceed else first initialise git using “git init” command

{% highlight ruby %}
git init
{% endhighlight %}
3.  Assuming you are in the directory where you have initialise git. Open “post-commit” file like

{% highlight ruby %}
mate .git/hooks/post-commit
{% endhighlight %}
4.  Type this and save the file.

{% highlight ruby %}
afplay ~/.git/happykids.wav > /dev/null 2>&1 &
{% endhighlight %}
5.  Go to you home directory by just typing

{% highlight ruby %}
cd
{% endhighlight %}
6.  create a hidden directory git ie

{% highlight ruby %}
mkdir .git
{% endhighlight %}
7.  Navigate to that directory ie:
{% highlight ruby %}
cd .git
{% endhighlight %}
8.  Download the sound file in that directory ie:
{% highlight ruby %}
wget http://collectiveidea.com/assets/4c58e4c1dabe9d50eb000087/happykids.wav
{% endhighlight %}
9.  Now go back to your project directory and make a commit..:)


Source: [http://collectiveidea.com/blog/archives/2010/08/03/happy-git-commits/][2]

 [2]: http://collectiveidea.com/blog/archives/2010/08/03/happy-git-commits/ "Source"
