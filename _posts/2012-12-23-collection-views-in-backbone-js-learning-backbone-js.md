---
title: 'Collection views in backbone js - Learning Backbone js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 9 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

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

In the previous lesson, we learned how to use the collection in Backbone js. Now in this topic, we will learn how to generate collection views in Backbone js. Let's start coding.

## What we have till now

So from the previous lesson we have:
{% highlight javascript %}

  // Person Model
  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 30,
          occupation: 'worker'
      }
  });

  // A List of People
  var PeopleCollection = Backbone.Collection.extend({
      model: Person
  });

  // The View for a Person
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

  var peopleCollection = new PeopleCollection([
      {
          name: 'Mohit Jain',
          age: 26
      },
      {
          name: 'Taroon Tyagi',
          age: 25,
          occupation: 'web designer'
      },
      {
          name: 'Rahul Narang',
          age: 26,
          occupation: 'Java Developer'
      }
  ]);

{% endhighlight %}

## Three things we need

* Person Model
* Person View
* Person Collection

So we have person model, person view, but the problem is we dont have collection view, a view that collects all smallers view and make it a complete giant view. Lets define one:

## Defining a collection

{% highlight javascript %}

  // View for all people
  var PeopleView = Backbone.View.extend({
      tagName: 'ul'
  });

{% endhighlight %}

We defined a PeopleView and as we are using `li` tag for small view is PersonView that why we defined tagName: `ul` in PeopleView. Now we need to define a render method which should be these functionalities.

*   Loop over all the person objects
*   Should call render for the person objects
*   Should display a collection as HTML




## Defining render method

So lets just define our render method and implement all of the above functionality one by one.

{% highlight javascript %}

  // View for all people
  var PeopleView = Backbone.View.extend({
      tagName: 'ul',

      render: function(){
      // must do certain things as specified above.
      //Loop over all the person objects
      //Should call render for the person objects
      //Should display a collection as HTML
      }
  });

{% endhighlight %}

Let's create a new object i.e., peopleView and see few things on Chrome developer tools console. I have added initialize function in CollectionView and here is the code for main.js

{% highlight javascript %}

  // Person Model
  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 30,
          occupation: 'worker'
      }
  });

  // A List of People
  var PeopleCollection = Backbone.Collection.extend({
      model: Person
  });


  // View for all people
  var PeopleView = Backbone.View.extend({
      tagName: 'ul',

      initialize: function(){
          console.log(this.collection);
      },

      render: function(){

      }
  });

  // The View for a Person
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

  var peopleCollection = new PeopleCollection([
      {
          name: 'Mohit Jain',
          age: 26
      },
      {
          name: 'Taroon Tyagi',
          age: 25,
          occupation: 'web designer'
      },
      {
          name: 'Rahul Narang',
          age: 26,
          occupation: 'Java Developer'
      }
  ]);

  // on console

  // var peopleView = new PeopleView({ collection: peopleCollection });

{% endhighlight %}

Here is the result from console:
![collection views in backbone js](/wp-content/uploads/Screen-Shot-2012-12-23-at-5.47.44-AM.png?fit=725,680)

*   So what I can see is three objects in the collection view
*   Lots of functions that can be applied to collection views.

So let's move ahead and use each function and loop over the collection view. Lets for now just run a loop.

{% highlight javascript %}

  // loop over all the person objects in the peopleCollection
  render: function(){
      this.collection.each(function(person){
              console.log(person);
      });
  }

{% endhighlight %}

So first step of looping is done. Now let's move ahead of the second step i.e., Create a view for each person.

{% highlight javascript %}

  // loop over all the person objects in the peopleCollection
  render: function(){
      this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              console.log(personView.el);
      });
  }

{% endhighlight %}

So far its fine. Now just hold a sec and checkout this carefully. “this” inside the loop lost the reference of the actual collection. Try out these two things to understand it a better way and checkout inline comments.

{% highlight javascript %}

  // loop over all the person objects in the peopleCollection
  render: function(){
          console.log(this); // reference to collection object.. Pretty useful..
      this.collection.each(function(person){
              var personView = new PersonView({ model: person });

      });
  }

  //OR


  // loop over all the person objects in the peopleCollection
  render: function(){
      this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              console.log(this);  // referencing to global window object and its pretty useless..
      });
  }

{% endhighlight %}

So to maintain the reference use this:(*checkout inline comments.*)

{% highlight javascript %}

  // loop over all the person objects in the peopleCollection
  render: function(){
      this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              console.log(personView.el);
      }, this);    // at this point we are passing context.. Underscore provides this functionality..
  }

{% endhighlight %}

So now we have a reference of original collection view inside the loop. So now just lets complete the third task, i.e., rendering the whole collection list.

{% highlight javascript %}

  var PeopleView = Backbone.View.extend({
      tagName: 'ul',

      render: function(){
          this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              this.$el.append(personView.el); // adding all the person objects.
          }, this);
      }
  });


  // on console

  //var peopleView = new PeopleView({ collection: peopleCollection });
  //peopleView.render();
  //peopleView.el;

{% endhighlight %}

Here is console output:

![collection views in backbone js](/wp-content/uploads/Screen-Shot-2012-12-23-at-6.08.39-AM.png?fit=678,392)

**A quick tip:** Always return this from your render method to do chaining. For example person.render.el instead of running two commands person.render and then person.el.


So let's use this tip finish up the lesson. So currently we have: (*checkout inline comments.*)

{% highlight javascript %}

  // Person Model
  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 30,
          occupation: 'worker'
      }
  });

  // A List of People
  var PeopleCollection = Backbone.Collection.extend({
      model: Person
  });


  // View for all people
  var PeopleView = Backbone.View.extend({
      tagName: 'ul',

      render: function(){
          this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              this.$el.append(personView.el);
          }, this);
      }
  });

  // The View for a Person
  var PersonView = Backbone.View.extend({
      tagName: 'li',

      template: _.template($('#personTemplate').html()),

      initialize: function(){
          this.render();
      },

      render: function(){
          this.$el.html( this.template(this.model.toJSON()));
      }
  });

  var peopleCollection = new PeopleCollection([
      {
          name: 'Mohit Jain',
          age: 26
      },
      {
          name: 'Taroon Tyagi',
          age: 25,
          occupation: 'web designer'
      },
      {
          name: 'Rahul Narang',
          age: 26,
          occupation: 'Java Developer'
      }
  ]);

{% endhighlight %}

Let's do certain things: (*checkout inline comments.*)

*   Remove initialize function from PersonView to use chaining and manually call render.
*   Returning this from PersonView render method
*   Returning this from CollectionView render
*   Adding the whole list on Dom for demo purpose.

{% highlight javascript %}

  // Person Model
  var Person = Backbone.Model.extend({
      defaults: {
          name: 'Guest User',
          age: 30,
          occupation: 'worker'
      }
  });
  // A List of People
  var PeopleCollection = Backbone.Collection.extend({
      model: Person
  });
  // View for all people
  var PeopleView = Backbone.View.extend({
      tagName: 'ul',
      render: function(){
          this.collection.each(function(person){
              var personView = new PersonView({ model: person });
              this.$el.append(personView.render().el); // calling render method manually..
          }, this);
          return this; // returning this for chaining..
      }
  });
  // The View for a Person
  var PersonView = Backbone.View.extend({
      tagName: 'li',
      template: _.template($('#personTemplate').html()),
         //////////   initialize function is gone from there. So we need to call render method manually now..
      render: function(){
          this.$el.html( this.template(this.model.toJSON()));
          return this;  // returning this from render method..
      }
  });
  var peopleCollection = new PeopleCollection([
      {
          name: 'Mohit Jain',
          age: 26
      },
      {
          name: 'Taroon Tyagi',
          age: 25,
          occupation: 'web designer'
      },
      {
          name: 'Rahul Narang',
          age: 26,
          occupation: 'Java Developer'
      }
  ]);
  var peopleView = new PeopleView({ collection: peopleCollection });
  $(document.body).append(peopleView.render().el);   // adding people view in DOM.. Only for demo purpose...

{% endhighlight %}

So lets just run this code and see what we have:

![Collection views in backbone js](/wp-content/uploads/Screen-Shot-2012-12-23-at-6.08.39-AM.png?fit=678,392)

Boom.. A complete list of the person displayed on the page. Pretty nice. ;) So now if you are the thing that so far so much code just to see a list. Hold on. This is how we got the whole structure of the application. Now to add Jquery events all we need to call functions and add some new minor features. Trust me once you start checking out jquery events. You will just fell in love with backbone.


***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
