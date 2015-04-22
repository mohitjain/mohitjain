---
title: Better way to see info using git log alias
author: Mohit Jain
layout: post
permalink: /2012/12/better-way-to-see-info-using-git-log-alias/



categories: Git tips-and-tricks
---

I am big fan of  git log command. Tells me lot of information, but I not impressed with the way it shows the information. I got a pretty big alias to improve and which makes things much better.


## Result


![Git log alias](/wp-content/uploads/2012/12/Screen-Shot-2012-12-09-at-12.50.56-AM.png)
Git log alias

Just gimme one liner:

{% highlight ruby %}
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)%Creset' --abbrev-commit --date=relative"
{% endhighlight %}
And now just type

{% highlight ruby %}
git lg
{% endhighlight %}
to see the result as the command will create a git log alias. See this [stackoverflow][3] question for more info on git log alias.

 [3]: http://stackoverflow.com/questions/1057564/pretty-git-branch-graphs "Git log Alias"

For more colors add this code in your .gitconfig in home directory.
{% highlight ruby %}
    [color]
        ui = auto
        interactive = auto
{% endhighlight %}

## New Output

![Better Git log alias](/wp-content/uploads/2012/12/Screen-Shot-2012-12-09-at-1.50.47-AM.png?fit=950,658)
