---
layout: post
description: How to encrypt and decrupt keys and other strings in ruby on rails.
title: "How to encyrpt and decrypt data in ruby on rails"
date: 2013-04-18 22:44
keywords: decryption, encryption, ruby on rails
categories:  encryption-and-decryption
---


[AESCrypt](https://github.com/Gurpartap/aescrypt) is a simple gem to encryption and decryption in ruby on rails. From the readme file.

##Installation

Add this line to your application's Gemfile:

{% highlight ruby %}

gem 'aescrypt'

{% endhighlight %}

<!--more-->

and run bundler

##Usage

{% highlight ruby %}

message = "top secret message"
password = "this_is_a_secret_key_that_you_and_only_you_should_know"

{% endhighlight %}

##Encrypting

{% highlight ruby %}

encrypted_data = AESCrypt.encrypt(message, password)

{% endhighlight %}

##Decrypting

{% highlight ruby %}

message = AESCrypt.decrypt(encrypted_data, password)

{% endhighlight %}

