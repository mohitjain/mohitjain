---
title: 'Namespacing in backbone js - Learning backbonejs'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---


> This entry is part 11 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

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


So far we declared everything as a global function i.e., Person, PersonView, PersonCollection, etc. Namespacing helps us to structure our application in the much nicer way and keep the application with limited global variables.

## Quick Look

Take a look on this.

{% highlight javascript %}

  (function(){

  window.App = {
      Models: {},
      Collections: {},
      Views: {}
  };

  window.template = function(id){
      return _.template( $('#' + id).html() );
  };
  })();

{% endhighlight %}

In the above code, we specified App as a name space. You can define what ever you want to as per your project name. And in the App namespace, we specified some other name space i.e., Models, Collections, Views. You can define templates if you have multiple templates. But for this example, I keep template as a totally different global variable.

## Understanding the namespacing

Cool. Now let's take a look at our current naming conventions, We have

{% highlight javascript %}

  Person
  PersonView
  PeopleCollection
  PeopleView

  // following the same now with namespace.

  App.Models.Person
  App.Views.PersonView
  App.Collections.PeopleCollection
  App.Views.PeopleView

  // The above code is ok, but there is redundancy in the naming which can be improved like this:

  App.Models.Person
  App.Views.Person
  App.Collections.People
  App.Views.People

{% endhighlight %}




## Implementation of namespace

So here is the new `main.js` file using namespacing in backbone js. *(Please check inline comments..)*


{% highlight javascript %}

  (function(){  // whole blocked is wrapped into anonymous Jquery function..

  window.App = {   // defining app name space, You can rename it as per your project name..
      Models: {},
      Collections: {},
      Views: {}
  };

  window.template = function(id){
      return _.template( $('#' + id).html() );
  };


  // Person Model
  App.Models.Person = Backbone.Model.extend({   // Person model referencing the App namespace model.
      defaults: {
          name: 'Guest User',
          age: 30,
          occupation: 'worker'
      }
  });

  // A List of People
  // Same here. People is referencing now collection from App namespace
  App.Collections.People = Backbone.Collection.extend({
      model: App.Models.Person   // Change here for Person Reference from App models namespace
  });


  // View for all people
  /// Same here. People is referencing now views from App namespace
  App.Views.People = Backbone.View.extend({
      tagName: 'ul',

      render: function(){
          this.collection.each(function(person){
                          // Change here for Person Reference from App Views namespace
              var personView = new App.Views.Person({ model: person });
              this.$el.append(personView.render().el);
          }, this);

          return this;
      }
  });

  // The View for a Person
  // Change here for Person Reference from App Views namespace
  App.Views.Person = Backbone.View.extend({
      tagName: 'li',

      template: template('personTemplate'),
      render: function(){
          this.$el.html( this.template(this.model.toJSON()));
          return this;
      }
  });
  // Change here for Person Reference from App Collections namespace
  var peopleCollection = new App.Collections.People([
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

  // Change here for Person Views from App Views namespace
  var peopleView = new App.Views.People({ collection: peopleCollection });
  $(document.body).append(peopleView.render().el);
  })();

{% endhighlight %}

Now just refresh your page and you will see same collections views output but in much nicer way. ;) Thats all for Namespacing in backbone js. Stay tuned for next lesson ie. Jquery Dom events. On Click events etc. Super excited for that lesson. ;)

***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
