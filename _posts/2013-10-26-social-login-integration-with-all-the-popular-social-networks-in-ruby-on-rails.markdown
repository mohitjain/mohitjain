---
layout: post
title: "Social Login integration with all the popular social networks in ruby on rails"
date: 2013-10-26 23:38
description: Rails – Twitter and Facebook, Google, Linkedin,  Github Authentications with Omniauth and Devise
categories: devise linkedin facebook google github twitter
keywords: facebook login with devise, google login with devise, github login with devise, linkedin login with devise,twitter login with devise,multiple social logins with rails and devise,facebook login with rails, google login with rails, github login with rails, linkedin login with rails,twitter login with rails
---

I have seen a lot of people writing pretty messy code to integrate social logins in rails or get confused to integrate multiple social logins in rails. In order to help them, I have written a small application having integrations with Twitter + Facebook + Linkedin + Google + Github.


Here is the [demo][1] and here is the [source code][2]

 [1]: http://social-login-in-rails.herokuapp.com/
 [2]: https://github.com/mohitjain/social-login-in-rails

I am using devise gem in this application. Few things to note in this:

1. There are two models in this application a user model and an authorizations model and a user has_many authorizations.
2. User can link to multiple social accounts from edit profile
3. Once social accounts are linked, the user can log in from any connected social network.
4. If the user tries to create an account with a different social network while in the logged out state. System maps it to the same account if that email address exists in the database else it will create a new account.
5. Twitter doesn't provide an email address of the user, nothing I can do about it.
6. There are a lot of other commented out gems in the Gemfile. Those are the gems that I use a lot in my various projects. I will strongly suggest you check out those gems.

<!--more-->

##How to replace and find keys to make this application work.

In the config directory, there is a file ie social_keys.yml. You need to specify all the social keys there. Make sure have restarted the application after making any change in that file.

Here are the URLs from where you can create an app and get the keys

##Facebook:

URL: [https://developers.facebook.com/apps](https://developers.facebook.com/apps)

Settings:


![Facebook Settings](/wp-content/images/facebook.png)


##Twitter:
URL: [https://dev.twitter.com/apps](https://dev.twitter.com/apps)

Settings: Enter call back URL as http://127.0.0.1:3000/twitter under settings tab once you create an application

##Google:
URL: [https://code.google.com/apis/console/b/0/?pli=1](https://code.google.com/apis/console/b/0/?pli=1)

Settings: Go to API Access and enter redirect URL as http://localhost:3000/users/auth/google_oauth2/callback


##Github:
URL: [https://github.com/settings/applications/new](https://github.com/settings/applications/new)

Settings: Application callback URL should be http://localhost:3000/users/auth/github


##Linkedin:
url: [https://www.linkedin.com/secure/developer](https://www.linkedin.com/secure/developer)

No settings required by default.
