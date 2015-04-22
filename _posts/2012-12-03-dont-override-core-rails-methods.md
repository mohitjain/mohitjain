---
title: 'Don&#8217;t override core Rails methods'
author: Mohit Jain
layout: post
permalink: /2012/12/dont-override-core-rails-methods/

categories: tips-and-tricks
---

Every one makes mistakes, mistakes that they never forget, cause they are so stupid and you can just smile to see those mistakes. Today I made one and they messed things so badly that it took me 5 hours to figure why its happening.
Mistakes were pretty simple but hard to figure out cause I made a method ie destroy in a model and a scope update in another one and screwed up everything. Don’t override core Rails methods like create, new, update destroy etc in any models. Shit happens..
