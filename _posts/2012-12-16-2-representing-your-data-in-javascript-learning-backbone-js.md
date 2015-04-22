---
title: '2. Representing your data in javascript &#8211; Learning Backbone js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 2 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

## Agenda
In this topic we will not be actually discussing about backbone, We will be learning how to represent data. We are using the same application that we build in previous blog post and building on top of it. Lets create a new file ie main.js and lets include that in `index.html`.

## Defining the object

Now lets define an object Person which has some attributes like name, age or occupation. Here is the code for that.

{% highlight javascript %}

var Person = function(config){
  this.name = config.name;
  this.age = config.age;
  this.occupation = config.occupation;
};

Person.prototype.work = function(){
	return this.name + 'is working.';
};

{% endhighlight %}
So why we are defining in this way is clear because we want to give a structure. Classes and objects are the best way to define a structure. So in the code sample above we defined a class Person and a function work. Save the file and open `index.html` file on browser. *(Make sure you have included main.js file in `index.html`)*

## Fire up the console and fire these commands

So from chrome developer console you can trigger following things to see some results.

{% highlight javascript %}

var person = new Person({name: "Mohit Jain", age: 25, occupation: "Software Developer"})
// this will create a new person object and then will set some attributes of that object.
person.name          // will give you the name of the person
person.age           // will give you the age of the person
person.occupation    // will give the occupation of the person.
person.work();      // will return the output of the function ie work defined in the main.js

{% endhighlight %}

Cool. Lets take a look on the screenshot explaining things on chrome console.

## Output on Chrome Console

![Representing your data – Chrome Console Output](/wp-content/uploads/2012/12/Screen-Shot-2012-12-16-at-8.25.50-AM.png)

Thats the basic way to give a better structure your code. Thats all in representing your data in javascript. Lets move forward and define first model in your backbone application.

***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
