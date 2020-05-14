---
title: 'How to improve templates in backbone js - Learning backbone js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 7 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

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

So in the previous lesson, we learned how to create templates. It good but it can be improved further using external templates. So in the lesson, we will learn how to develop templates in backbone js.

## What we have till now

From the previous episode, we have this PersonView class

{% highlight javascript %}

  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest Worker',
          age: 23,
          occupation: 'worker'
      }
  });

  var PersonView = Backbone.View.extend({
      tagName: 'li',

      my_template: _.template("<strong><%= name %></strong> (<%= age %>) - <%= occupation %>"),

      initialize: function(){
          this.render();
      },

      render: function(){
          this.$el.html( this.my_template(this.model.toJSON()));
      }
  });

  // calls from console

  // var person = new Person;  // a person object created...
  // var personView = new PersonView({ model: person });
  // personView.el   // ---->; You can call this method and it will display the view..
  //$(document.body).html(personView.el);  //  --->; This will add output to the dom. This is not ideal but good enough for demo.

{% endhighlight %}

So now we will take the template HTML code out into an external file and then call it here in out template. So let's use index.html file and define a template there. So just paste this code in your `index.html` file

{% highlight javascript %}

  <script id="personTemplate" type="text/template">
      <strong><%= name %></strong> (<%= age %>) - <%= occupation %>
  </script>

{% endhighlight %}

We have defined this script as `text/template` so that browser doesn't execute this as standard javascript code. So once we have set the template, we can call this external template in our PersonView file using jquery. Here is the new `PersonView` Class.

{% highlight javascript %}

  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 23,
          occupation: 'worker'
      }
  });

  var PersonView = Backbone.View.extend({
      tagName: 'li',

      template: _.template( $('#personTemplate').html()),

      initialize: function(){
          this.render();
      },

      render: function(){
          this.$el.html( this.template(this.model.toJSON()));
      }
  });

  // calls from console

  // var person = new Person;  // a person object created...
  // var personView = new PersonView({ model: person });
  // personView.el   // ---->; You can call this method and it will display the view..
  //$(document.body).html(personView.el);  //  --->; This will add output to the dom. This is not ideal but good enough for demo.

{% endhighlight %}



## Output on Chrome Console

Pretty nice right. Now lets what we have on chrome developer tools.

![Defining external templates in backbone js](/wp-content/uploads/defining-templates-in-backbone-js.png)

Similarly what we had in the previous lesson. Beautiful and cool. So this makes our life much easier to define the templates in an external file and then just call it when we need it. And we can structure out HTML code of the template pretty easily.


That's all for this lesson. Now thing about one object. How about displaying multiple objects. `ul` and `li` tags. The good thing is backbone js has collection view for that. Let's see that in next lesson.

***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
