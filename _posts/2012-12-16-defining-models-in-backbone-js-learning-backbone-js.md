---
title: Defining models in backbone js – Learning Backbone js
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---


> This entry is part 3 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

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

In the previous lesson, we created a Person Class. So if we want to define the same class in backbone js. And that's what we will be learning in this lesson. “Defining models in Backbone js.” It's pretty straight forward. Remove the previous code from `main.js` and add this code. Take a look on this.

{% highlight javascript %}

  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 23,
          occupation: 'Worker'
      },
      work: function(){
          return this.get('name')  +  'is working.';
      }
  });

{% endhighlight %}

In the above code, we are defining the class and set some default values like for name, age, and occupation.

## Fire up the console and fire these commands
Now if checkout chrome we can see a lot of cool awesome things. Type these commands one by one.

{% highlight javascript %}

  var person = new Person;  // creating a new object

  person  // printing that object. -> Notice output of this.

  // 1. We have access to attributes,
  // 2. We have access to functions,
  // 3. We have access to changed object, which helps us to check if the object has been changed or not.
  // 4. If something has been changed then backbone will announce that thing and
  // 5. we can hook into that to update DOM or do other cool things.

{% endhighlight %}


## Getters

We can get all the previous things like to get the name, age or occupation. In backbone js, we do that by using get method


{% highlight javascript %}

  person.get('name')// will display the name ie Default User
  person.get('age')// will display the age  ie 23
  person.get('occupation')// will display the occupation ie Worker

{% endhighlight %}

You **can’t** do things like:

{% highlight javascript %}

  person.name // THATS invalid..
  person.age  // THATS invalid..

{% endhighlight %}

## Setters

And now you can even update name, or age, etc.

{% highlight javascript %}

  person.set('name', 'Taroon Tyagi')// will update the name
  person.set('age', 26)             // will update the age
  person.set('occupation', 'Graphics Designer')// will update the occupation

{% endhighlight %}

or you can update the values in just on go ie

{% highlight javascript %}
  person.set({name:"Taroon Tyagi", age: 26, occupation: "Graphics Designer"})
{% endhighlight %}


## Set values while initiating object

Another thing can be you can set values while launching, i.e.,

{% highlight javascript %}

  var person = new Person({name:"Taroon Tyagi", age: 26, occupation: "Graphics Designer"})

{% endhighlight %}

## One last point - JSON output

{% highlight javascript %}

  person.toJSON(); // this will return all the attributes of that object. It will not return a Json be returned what we need :)

{% endhighlight %}

## Output on Chrome Console

Let's take a look how things look like on chrome console.

![Defining models in in backbone js](/wp-content/uploads/Defining-models-in-in-backbone-js.png)

That's how you define models in Backbone js. In the next post, let's add some validations in the model. For example. Age can’t be zero or negative. Or name can’t be blank etc.

***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
