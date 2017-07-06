---
title: '1. Introduction to backbone js and setting up an working environment &#8211; Learning Backbone js'
author: Mohit Jain
layout: post
comments: true
banner_image: "/media/backbone.jpg"
featured: true
categories: Backbone.js
---

> This entry is part 1 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

* [Introduction and Installation](/2012/12/introduction-to-backbone-js-and-setting-up-an-working-environment)
* [Representing your data in javascript](/2012/12/2-representing-your-data-in-javascript-learning-backbone-js)
* [Defining Models in backbone js](/2012/12/3-defining-models-in-backbone-js-learning-backbone-js)
* [Adding Validations in models backbone js ](/2012/12/4-adding-validations-in-models-in-backbone-js-learning-backbone-js)
* [Explaining views in backbone js](/2012/12/5-explaining-views-in-backbone-js-learning-backbone-js)
* [How to use templates in backbone js ](/2012/12/how-to-use-templates-in-backbone-js-learning-backbone-js)
* [How to improve templates in backbone js](/2012/12/how-to-improve-templates-in-backbone-js-learning-backbone-js)
* [Collections in backbone js](/2012/12/8-collections-in-backbone-js-learning-backbone-js)
* [Collection views in backbone js ](/2012/12/9-collection-views-in-backbone-js-learning-backbone-js)
* [Template helpers in backbone js](/2012/12/template-helpers-in-backbone-js-learning-backbonejs)
* [How to use namespace in backbone js ](/2012/12/11-namespacing-in-backbone-js-learning-backbonejs)
* [How to handle dom events in backbone js and define your custom events](/2012/12/12-listening-to-dom-events-in-backbone-js-learning-backbone-js) ([Live Demo](http://listen-dom-events-backbone.herokuapp.com))
* [Routing in backbone js](/2013/01/routers-in-backbone-js-learning-backbone-js)

***

So this is a series of posts explaining backbone js. I am hoping for feedback on each to make it better. At the end of each post, you can find a link to download the source code.


## What is backbone js.

Backbone.js is an uber-light framework that allows you to structure your Javascript code in a **MVC**(Model, View, Controller) fashion where…

*   **Model** is part of your system that retrieves and populates the data,
*   **View** is the HTML representation of this model(views change as models change, etc.)
*    **Controller** that in this case allows you to save the state of your javascript application via a hashbang URL, for example: 

## Why and when we need to use it.

Whenever you feel you using tons of lines of javascript (or jquery) in your application for example. Do this when this happens, then make an ajax request, then show some animation, then replace the dom elements and so on. Then you keep adding more and more lines of code, and it becomes a mess. I have worked on a couple of projects in which I have done the same thing cause those applications are so much front end dependent. Designers keep suggesting better and better designs, and then we start writing tons of jquery code without any structure. If you are doing the same then checkout backbone. It will help you for sure by giving you a structure to your javascript code.



## What are the various dependencies that I need to use.

As per the default, the only dependency is underscore js, which provides a lot of helper methods and jquery. So in this, I will be using underscore js and jquery and will try to cover few things related to the coffee script, etc. I will be using Chrome browser and use Chrome console to try out various things.

## Installation:

So to setup a working environment, You need three js files

1. [Jquery][1]
2. [Backbone][2]
3. [Underscore][3]

 [1]: http://jquery.com/ "Jquery Library Download"
 [2]: http://documentcloud.github.com/backbone/ "Backbone library download"
 [3]: http://underscorejs.org/ "Underscore Library download"

## Loading Backbone js

So once downloaded I will create a js folder for all the js and index.html file which loads all the libraries.

{% highlight HTML %}

<!DOCTYPE html>
<html lang="en">
    <head>
      <meta charset="utf-8">
    </head>
    <body>
      <script src="js/underscore.js"></script>
      <script src="js/jquery.js"> </script>
      <script src="js/backbone.js"></script>
    </body>
</html>

{% endhighlight %}

## Testing in browser

Now open you index.html file in chrome and open chrome developer tools and open console tab, and if installation is proper then you should have access to global variable Backbone

![Backbone Load test](/wp-content/uploads/2012/12/Screen-Shot-2012-12-16-at-5.30.02-AM.png)

That's all in the installation. Let's start the journey :)

***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
