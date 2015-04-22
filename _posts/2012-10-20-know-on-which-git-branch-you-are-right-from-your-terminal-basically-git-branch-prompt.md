---
title: Know on which git branch you are, right from your terminal, basically git branch prompt
layout: post



permalink:  /2012/10/know-on-which-git-branch-you-are-right-from-your-terminal-basically-git-branch-prompt/
description: display git branch in terminal prompt
keywords: git, terminal, tips and tricks
categories: Git tips-and-tricks
---

If you are using Git or Gitflow probably you keep switching between various branches. If you want to see what branch you are on, right from your terminal instead to typing command i.e. git branch.

##Run these commands:
{% highlight ruby %}
mkdir ~/.bash
cd ~/.bash
git clone git://github.com/mikesten/git-aware-prompt.git
{% endhighlight %}
Edit your ~/.profile or ~/.bash_profile and add these lines on the top of the file.
{% highlight ruby %}
export GITAWAREPROMPT=~/.bash/git-aware-prompt
source $GITAWAREPROMPT/main.sh
export PS1="u@h w[$txtcyn]$git_branch[$txtylw]$git_dirty[$txtrst]$ "
{% endhighlight %}
Restart your terminal and then you will see the output like this

![Git brancg info on terminal](/wp-content/uploads/2012/10/b588e9e1480c94802e4860b5fd2d0f82.png?fit=360,65)
