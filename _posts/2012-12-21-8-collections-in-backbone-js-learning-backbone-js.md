---
title: '8. Collections in backbone js &#8211; Learning Backbone js'
author: Mohit Jain
layout: post
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---


> This entry is part 8 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

So from previous lessons we know how to create a Person model, We know how to create PersonView and we how to define inline and external templates. In this lesson we will learn collections in backbone js and in lesson we will learn how define views for collections in backbone js.

## What we have till now

So here is the code that we have from previous lesson.

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

## Defining a collection

Now from above code if we want to create a new person and add that model in view that it will become messy and it will go so much messy if we have to define some 10 people records. Thanks to backbone that we have collections in backbone js. So here is how we define collections in backbone js.

{% highlight javascript %}
// A List of People
var PeopleCollection = Backbone.Collection.extend({
	model: Person
});

{% endhighlight %}

## Setting up the defaults

So we tell collection that what kind of objects we are dealing with by specifying model attribute. In this case we have PeopleCollection so we have Person defined there. So lets see how to can use it. So we have:

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

{% endhighlight %}

## Fire up the console and fire these commands

{% highlight javascript %}

 var person = new Person;
 var personView = new PersonView({ model: person });
 var peopleCollection = new PeopleCollection();
 peopleCollection.add(person);
 var person2 = new Person({name: "Mohit Jain", age: 25, occupation: "Software Developer"});
 var personView2 = new PersonView({ model: person2 });
 peopleCollection.add(person2);
 peopleCollection
 peopleCollection.toJSON(); // --> returns a list of data attributes

{% endhighlight %}

## Output on Chrome Console

Lets see what we have on console.

![Collections in backbone js](/wp-content/uploads/2012/12/Screen-Shot-2012-12-21-at-1.11.41-AM.png?fit=690,614)


<!--more-->


## Another way of adding data in collection

Another way to adding data in collections is:

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


So you can loop over it. Do so many things as collections has so much data stored in it with respect to model objects. It may seem like we can store in the form of array but collections have their collections view and that make them pretty powerful. Lets talk about collection views in next lesson and that will help you to understand the importance of collections.

***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
