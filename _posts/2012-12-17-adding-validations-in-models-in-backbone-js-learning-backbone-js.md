---
title: Adding Validations in models in backbone js – Learning Backbone js
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js Validations
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 4 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

* [Introduction and Installation](/introduction-to-backbone-js-and-setting-up-an-working-environment)
* [Representing your data in javascript](/representing-your-data-in-javascript-learning-backbone-js)
* [Defining Models in backbone js](/defining-models-in-backbone-js-learning-backbone-js)
* [Adding Validations in models backbone js ](/adding-validations-in-models-in-backbone-js-learning-backbone-js)
* [Explaining views in backbone js](/explaining-views-in-backbone-js-learning-backbone-js)
* [How to use templates in backbone js ](/how-to-use-templates-in-backbone-js-learning-backbone-js)
* [How to improve templates in backbone js](/how-to-improve-templates-in-backbone-js-learning-backbone-js)
* [Collections in backbone js](/collections-in-backbone-js-learning-backbone-js)
* [Collection views in backbone js ](/collection-views-in-backbone-js-learning-backbone-js)
* [Template helpers in backbone js](/template-helpers-in-backbone-js-learning-backbonejs)
* [How to use namespace in backbone js ](/namespacing-in-backbone-js-learning-backbonejs)
* [How to handle dom events in backbone js and define your custom events](/listening-to-dom-events-in-backbone-js-learning-backbone-js) ([Live Demo](http://listen-dom-events-backbone.herokuapp.com))
* [Routing in backbone js](/2013/01/routers-in-backbone-js-learning-backbone-js)

***

## Agenda

So in previous post, we defined a person class with some default values in it. Now I want to add some validations like, Age can’t be negative, or name can’t be blank. Let's start adding Validations in models in Backbone js.


## What we have till now

So we have a person model i.e.,
{% highlight javascript %}

  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 23,
          occupation: 'Worker'
      },
      work: function(){
          return this.get('name')  ' is working.';
      }
  });

{% endhighlight %}

## Defining the first validation

Now you can validations by using validate function like this:

{% highlight javascript %}

  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 23,
          occupation: 'worker'
      },

      validate: function(attributes){
          if ( attributes.age <  ){
              return 'Age must be positive.';
          }

          if ( !attributes.name ){
              return 'Every person must have a name.';
          }
      },

      work: function(){
          return this.get('name') + ' is working.';
      }
  });

{% endhighlight %}

## Fire up the console and fire these commands

Now, lets head back to chrome developer tools. In the console:

{% highlight javascript %}

  var person = new Person({name: "Mohit Jain", age: -1, occupation: "Software Developer"}) // This will not trigger validate method as validate method will be triggered only in case of set.
  person.get('age')// will return -1

  var person = new Person;
  person.get('age')// will return 23 as default value
  person.set('age', -1)// will return false and value ie -1 will not be set
  person.get('age')// will still return ie 23

  var person = new Person;
  person.get('age')// will return 23 as default value
  person.set('age', 18)// will return true and value ie 18 will be set
  person.get('age')// will return new value ie 18

{% endhighlight %}

## Displaying the error messages.

To see the errors messages, you have to bind a listen to the event to the person. A simple way to do that is:

{% highlight javascript %}

  person.on('error', function(model,error){
    console.log(error); // printing the error message on console.
  });

{% endhighlight %}

**Now if you say:**

{% highlight javascript %}

  person.set("age", -1)
  // it will return false and will show the error message.

{% endhighlight %}

## Output on Chrome Console

Cool. Let's see what we have on the console.

![adding validations in backbone models](/wp-content/uploads/adding-validations-in-backbone-models.png)

Pretty simple right? Let's move forward and see how to handle data presentation, i.e., views in Backbone js.


***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
