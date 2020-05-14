---
title: Rotating Rails Log Files
author: Mohit Jain
layout: post
comments: true
description: How to rotate ruby on rails on daily basics.
keywords:  logs, performance
categories: Performance Logs ruby-on-rails
---

### Why Rotation of log files is necessary.

The idea behind log rotation is simple: make a backup of the current log file, continue recording into a new or cleared log file, and discard log files that are older than a particular date.
Your web server probably already rotates its log files. For Apache, they are probably located in/etc/httpd/logs and they are probably rotated weekly. These logs store everything Apache does. Simple web server stats and traffic analysis tools make use of these log files to show who visits a site when and what pages are viewed.
While it is possible to configure your Rails application to log to your Apache log files, I do not think it is a good practice. It’s much better to give each Rails application its log file—it will be easier to find serious Rails errors, it will keep your Apache logs cleaner and Rails is set up to keep its logs by default. Fortunately, on a Linux server, the built-in log rotate program will make the process super-easy. After the jump, I’ll walk you through the steps to get it set up.
Configuring logrotate gets its configuration information from the file /etc/logrotate.conf. If you can’t find it, you can type locate logrotate.conf from the command line to see where it lives. Open up that file in a text editor (nano /etc/logrotate.conf will work) and append the following lines at the end:

{% highlight ruby %}

  # Rotate Rails application logs

  /path/to/your/rails/applicaton/log/*.log {
    daily
    missingok
    rotate 7
    compress
    delaycompress
    notifempty
    copytruncate
  }

{% endhighlight %}

# Here’s what each line do:

## /path/to/your/rails/applicaton/log/*.log –
 Use the full path to the log directory of your Rails application (symbolic links are acceptable too). “*.log” will rotate any file in the log directory with .log at the end. If you only want to rotate certain log files, you can be more specific.

## daily
 Rotates the log files every day. You could specify weekly or monthly instead.

## /missingok
 Don’t issue an error message if log files are missing.

## /rotate 7
 The maximum number of log files to keep. Once you have more than this number, the oldest file will be deleted. I set it to keep seven days worth but feel free to change this number.

## /compress
 Compress old versions of log files to save space (uses gzip by default).

## /delaycompress
 Delays the compression until the next log rotation. It’s a minor point and probably not strictly necessary, but it makes sure that the log file is truly no longer active before compressing it.

## /notifempty
 If the log file is empty, there’s no need to rotate it. You can remove this option if you want to rotate even blank log files; just keep in mind that you may erase a log file that has lots of information to make room for your empty log file.

## /copytruncate
 Makes a backup copy of the current log and then clears the log file for continued writing. The alternative is to use create which will perform the rotation by renaming the current file and then creating a new log file with the same name as the old file. I strongly recommend that you use copy truncate unless you know that you need to create. The reason why is that Rails, FastCGI, Mongrel, etc. may still keep pointing to the old log file even though its name has changed and they may require restarting to locate the new log file. copytruncate avoids this by keeping the same file as the active file.

If you have more than one Rails application, you can repeat this code to rotate them all one-after-another. Their other options you can specify, man logrotate will show you them all. I haven’t used them, but the options to mail log files on creation or deletion look attractive. It is also possible to have rotated the logs once they get to a certain size instead of at a particular time.

## Using logrotate

To use the log rotation you just configured, you have two choices.

1. Wait for the next day (or whatever period you specified). If you set it correctly, the rotation should occur automatically and without further commands.
2. Run it immediately by typing /usr/sbin/logrotate -f /etc/logrotate.conf on the command line. (The -f is for “force it to run now.)

That’s all there is to it! Now your log files won’t fill up to an unmanageable size yet you’ll still be able to go back and track any recent errors.
