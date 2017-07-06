---
title: Better coloured output for git diff
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/better-coloured-output-for-git-diff/
categories: Git quick-solution tips-and-tricks utilities
---
Last week I made a post regarding better git log. I learned from that and made some more modifications in my .gitconfig file (you can find it in your home directory) added some configurations to make a better colored out for git diff.

{% highlight ruby %}
git diff

{% endhighlight %}

**Here is my .gitconfig file:** (Change your name and email address.)

{% highlight ruby %}

[user]
    name = chnage_your_name_here
    email = change_it_to_your_email_address@gmail.com
[core]
    excludesfile = /Users/mohit/.gitignore_global
[color]
    ui = auto
    interactive = auto
     branch = auto
     diff = auto
     status = auto
[color "branch"]
     current = yellow reverse
     local = yellow
     remote = green
[color "diff"]
     meta = yellow bold
     frag = magenta bold
     old = red
     new = cyan
[color "status"]
    added = yellow
     changed = green
     untracked = cyan
[difftool "sourcetree"]
    cmd = opendiff "$LOCAL" "$REMOTE"
    path =
[mergetool "sourcetree"]
    cmd = /Applications/SourceTree.app/Contents/Resources/opendiff-w.sh "$LOCAL" "$REMOTE" -ancestor "$BASE" -merge "$MERGED"
    trustExitCode = true
[alias]
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)%Creset' --abbrev-commit --date=relative

{% endhighlight %}
