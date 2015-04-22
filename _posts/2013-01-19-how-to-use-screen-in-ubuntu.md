---
title: How to use screen in ubuntu
author: Mohit Jain
layout: post
permalink: /2013/01/how-to-use-screen-in-ubuntu/



categories: quick-solution Server tips-and-tricks utilities
---

Screen is a terminal multiplexer, which allows a user to access multiple separate terminal sessions inside a single terminal window or remote terminal session. Sometimes you need to run a rake task or something else which keep on producing logs and you want to keep it running even you close your terminal. To obtain this, create a .screenrc file in your home directory and paste the following code:

{% highlight ruby %}

hardstatus on
hardstatus alwayslastline
hardstatus string "%w%=%m/%d %c"

{% endhighlight %}
Save the file and now you can type screen to start a new screen. Press enter or space as guided and do whatever you want to. For example lets run a rake task on production server and let it run even if close our ssh terminal.

So go to your project directory and run RAILS\_ENV=production rake my\_awesome\_rake\_task. So now its running (assuming its a long task) You want to logout from the server and let this rake task running. So lets do it from scratch. Here are all the steps.


*   ssh user@server_ip
*   Create .screenrc file and paste the content as specified.
*   Now type screen to start a new screen. Hit space or enter key as guided
*   Now navigate to project directory and run RAILS\_ENV=production rake my\_awesome\_rake\_task and let it run there.
*   Now to detach the screen and come back to original terminal without closing the rake task. Press Contol a and then press control d
*   You will come back to the same orginal termainal and that rake task will keep on running in a screen
*   Now if you want to see the same rake task again type screen -r .This will resume the same previous screen
*   Once that rake task to done to kill the screen type exit
*   If you want to start a new screen type screen again and it will create a new screen
*   Ctrl-a Shift-A will help to rename a screen (the screen on which you are)

Thats all basic how to use screen in ubuntu. You can find a lot of things about screen in ubuntu from your best friend Google
In my few projects our screen is running for past 1.2 years :-), so its safe and smooth to run screens.
