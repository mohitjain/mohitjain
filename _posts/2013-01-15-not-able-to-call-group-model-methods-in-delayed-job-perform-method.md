---
title: Not able to call group model methods in delayed job perform method
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/not-able-to-call-group-model-methods-in-delayed-job-perform-method/
categories: quick-solution tips-and-tricks utilities
---

I was working on my project and got a very strange error. I was not able to call any group model methods in delayed job perform the method. Checking out wiki of delayed job I got this:

*There’s a strange edge-case with Ruby/Rails where Struct::Group already exists, so calling Group.anything from within a class that inherits from Struct will have strange results. You can workaround this issue by prefixing calls to Group with two colons. For example, ::Group.find or ::Group.other\_methods\_defined\_in\_model would work as expected*
