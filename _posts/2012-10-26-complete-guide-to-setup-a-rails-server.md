---
title: Complete guide to setup a rails server
author: Mohit Jain
layout: post
comments: true
permalink: /2012/10/complete-guide-to-setup-a-rails-server/

summary: extra_long

categories: Server
---


**This guide is written by Mohit Jain (http://codebeerstartups.com). It worked fine for me in more than 15 deployments. Use this guide at your own risk, if your server explode, it will not be my fault ;-)**

*If something went wrong, drop me message, I will try to help you :)*

##Stack

1.  Ubuntu .
2.  Rails 3
3.  Mysql
4.  Apache
5.  Passenger

##Step 1: (Creating a deployer account)

1.  Ssh into the system using the root credentials

{% highlight ruby %}
ssh root@ip_address
{% endhighlight %}
2.  Create new user/s and switch to that one.

{% highlight ruby %}

# Add deployer user - deployer is the username of the user you are creating. Change it as per your needs
adduser deployer --ingroup admin
su deployer
cd


OR

/usr/sbin/groupadd deployers  #Create new group for deployers
/usr/sbin/visudo
## Allows people in group deployers to run all commands
%deployers  ALL=(ALL)ALL
#Save and Exit.
/usr/sbin/adduser deployer  #Create new user
/usr/sbin/usermod -a -G deployers deployer  #Add deployer user to deployers group
#Logout and login as deployer
{% endhighlight %}
3.  (Optional but preferable). Logout using logout and login as deployer i.e.

{% highlight ruby %}
ssh deployer@ip_address
{% endhighlight %}

4.  Generate SSH keys and public key in deployment keys on github/bitbucket

{% highlight ruby %}
ssh-keygen -t rsa -C "your_email_address"
cat ~/.ssh/id_rsa.pub
{% endhighlight %}
5.  Copy your public key to authorised key, (SO that you don’t need to enter password next time when you try to login on server from your machine. DONT do this in case you don’t want to give this current machine access of the server.):

{% highlight ruby %}
cat ~/.ssh/id_rsa.pub | ssh deployer@your_ip 'cat >> ~/.ssh/authorized_keys'
{% endhighlight %}
**Step 2: (Preparing the stack)**

6.  Update and Upgrade the system

{% highlight ruby %}
sudo apt-get update
sudo apt-get upgrade
{% endhighlight %}
7.  Install MySQL and libmysqlclient16-dev [dependency for mysql2 gem]

{% highlight ruby %}
sudo apt-get install mysql-server mysql-client libmysqlclient16-dev
{% endhighlight %}

8.  Install Apache

{% highlight ruby %}
sudo apt-get install apache2
{% endhighlight %}
9.  Install Git, Curl and build-essential [to compile ruby]

{% highlight ruby %}
sudo apt-get install build-essential libxslt1.1 libxslt1-dev libxml2 ruby-full mysql-server libmysqlclient-dev libmysql-ruby libssl-dev libopenssl-ruby libcurl4-openssl-dev imagemagick libmagickwand-dev git-core redis-server libffi-dev libffi-ruby rubygems libsqlite3-dev libpq-dev libreadline5 openjdk-7-jre nodejs libncurses5-dev git-core openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev autoconf libc6-dev automake libtool bison  curl
{% endhighlight %}
10. Install RVM *I dont prefer that one liner for rvm ruby rails as i keep getting issue for readline etc.*

{% highlight ruby %}
bash < <(curl -sk https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
{% endhighlight %}
11. Reload bash_profile

{% highlight ruby %}
source ~/.bash_profile
{% endhighlight %}

12. Install ruby 1.9.3

{% highlight ruby %}
rvm pkg install openssl
rvm pkg install readline
rvm install 1.9.3 --with-openssl-dir=$rvm_path/usr --with-readline-dir=$rvm_path/usr
{% endhighlight %}
13. Make 1.9.3 the default interpreter

{% highlight ruby %}
rvm --default use 1.9.3
{% endhighlight %}
14. Install rails

{% highlight ruby %}
gem install rails --no-ri --no-rdoc
OR
gem install rails -v 3.2.16 --no-ri --no-rdoc

{% endhighlight %}
15. Install passenger

{% highlight ruby %}
gem install passenger --no-ri --no-rdoc
{% endhighlight %}
16. Install Apache2 module

{% highlight ruby %}
passenger-install-apache2-module
{% endhighlight %}
Press Enter and passenger-install will notify about the missing dependencies, Install them, and run the command again ie

{% highlight ruby %}
passenger-install-apache2-module
{% endhighlight %}
    Passenger will ask to paste some code in cofig file paste the output specified in apache config file ie:

{% highlight ruby %}
sudo vi /etc/apache2/apache2.conf
{% endhighlight %}
17. Other Packages: (Mail Servers, Image Magick and Search Engine) and some other dependencies

{% highlight ruby %}
sudo apt-get install imagemagick sphinxsearch  libmagickwand-dev libmagick9-dev postfix bsd-mailx libxslt-dev libxml2-dev
{% endhighlight %}
 **If you use postfix, then you fix it quickly by disabling tls by setting “smtpd\_use\_tls=no” in /etc/postfix/main.cf , else it will be keep throwing errors when rails will try to send email. Once settings has been changed, then just start the postfix ie:**


{% highlight ruby %}
sudo /etc/init.d/postfix start
{% endhighlight %}

18. Enable Rewrite module(if needed)

{% highlight ruby %}
sudo a2enmod rewrite
{% endhighlight %}
19. Restart Apache
{% highlight ruby %}
sudo /etc/init.d/apache2 restart
{% endhighlight %}
20. Config file: (You will need to for other changes later on.)
{% highlight ruby %}
sudo vi /etc/apache2/apache2.conf
{% endhighlight %}
** Typical Apache settings example for your apache config file.**

21. If you don’t have domain name yet then you can run your application on IP only.

{% highlight ruby %}

NameVirtualHost my_server_ip:80
<VirtualHost *:80>
ServerName my_server_ip
DocumentRoot /home/deployer/apps/my_awesome_rails_project/current/public
</VirtualHost>
{% endhighlight %}
22. You have a domain ie example.com and want to run application on that. Here is apache config code for that.

{% highlight ruby %}

NameVirtualHost my_server_ip:80
<VirtualHost *:80>
ServerName example.com
DocumentRoot /home/deployer/my_rails_app/production/current/public
</VirtualHost>
{% endhighlight %}
23. Redirect www requests to non – www, here is the code for that. Reverse of this ie redirect non www requests to www can be possible by making small modifications :)

{% highlight ruby %}

NameVirtualHost my_server_ip:80
<VirtualHost *:80>
ServerName example.com
RewriteEngine On
Redirect permanent / http://www.example.com

{% endhighlight %}

24. Wants to setup staging server? Here is the code for that running in different environment

{% highlight ruby %}

<VirtualHost *:80>
ServerName staging.example.com
RackEnv staging
DocumentRoot /home/deployer/my_rails_app/staging/current/public
  </VirtualHost>
Add expiry headers for all the assets.

sudo a2enmod expires
# make sure you restart the apache after adding anything in config file.
sudo service apache2 restart


<VirtualHost *:80>
ExpiresActive On
ExpiresByType image/gif "access plus 1 months"
ExpiresByType image/jpg "access plus 1 months"
ExpiresByType image/jpeg "access plus 1 months"
ExpiresByType image/png "access plus 1 months"
ExpiresByType image/vnd.microsoft.icon "access plus 1 months"
ExpiresByType image/x-icon "access plus 1 months"
ExpiresByType image/ico "access plus 1 months"
ExpiresByType application/javascript "now plus 1 months"
ExpiresByType application/x-javascript "now plus 1 months"
ExpiresByType text/javascript "now plus 1 months"
ExpiresByType text/css "now plus 1 months"
ExpiresDefault "access plus 1 days"
ServerName example.com
DocumentRoot /home/deployer/my_rails_app/production/current/public
</VirtualHost>
{% endhighlight %}

Will make a post soon for deploying your application with capistrano.
