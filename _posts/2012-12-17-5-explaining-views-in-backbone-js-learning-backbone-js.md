---
title: '5. Explaining views in backbone js &#8211; Learning Backbone Js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 5 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

In previous lessons we saw how to define models and add validations. In this lesson we will be checking out views in backbone js. Views are basically how you display your data.

## What we have till now

In order to make things simpler lets remove validations and functions from model. So we have this.

{% highlight javascript %}

var Person = Backbone.Model.extend({
	defaults: {
		name: 'Guest User',
		age: 23,
		occupation: 'worker'
	}
});

{% endhighlight %}

So now we want to add a view for a person. For simplicity lets take about list items. So every person will be displayed in a `li` tag. In order to define that view lets create a person view ie:

{% highlight javascript %}

var PersonView = Backbone.View.extend({
	tagName: 'li'
});

{% endhighlight %}

## Fire up the console and fire these commands

By default tagName is `div`. Here we specified it to use `li`. So if we see this output:


{% highlight javascript %}

var personView = new PersonView();
personView.el //will tell you the view for the object. Right now its a blank "li" tag.
personView.$el // is jquery tied up view for this object.

{% endhighlight %}


## Output on Chrome Console

Lets head back to chrome developer tools and see what we have in this object.

![Define a basic view](/wp-content/uploads/2012/12/Screen-Shot-2012-12-16-at-8.53.11-PM.png?fit=283,227)

## Adding html elements like class, id

You can also add other things like css class name, element id etc using some other attributes like

{% highlight javascript %}

var PersonView = Backbone.View.extend({
	tagName: 'li',
        className: 'person',
        id: 'person-id' // although this is not a good way but I think got the idea.
});
{% endhighlight %}

## Rendering the view

So backbone offers constructor for the views ie known as initialize ie it will be automatically called when you initiate a view.

{% highlight javascript %}
initialize: function(){
}
{% endhighlight %}

Backbone also offers a method render that will render out the output for the data of the model associated with that view. ie

{% highlight javascript %}

render: function(){
}

{% endhighlight %}

<!--more-->

So lets add all these in out class, so we have something like this:

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

   initialize: function(){
     this.render();
   },

   render: function(){
     this.$el.html( this.model.get('name') + ' (' + this.model.get('age') + ') - ' + this.model.get('occupation') );
  }
});

// calls from console

// var person = new Person;
// var personView = new PersonView({ model: person });
{% endhighlight %}

So in the above code we defined certain things.

*   initialize function that will called on PersonView initialization.
*   render method that add the content in the view
*   initialize function is calling render method which will add content in view.

## Fire up the console and fire these commands

Lets head towards chrome console and execute these commands to see what we have.

{% highlight javascript %}

var person = new Person;
var personView = new PersonView({ model: person });
personView.el;

// lets create a new person and display that person in view..
var person = new Person({name: "Mohit Jain", age: 25, occupation: "Software Developer"})
var personView = new PersonView({ model: person });
personView.el;
$(document.body).html(personView.el);  // this is not ideal but good enough for demo.
{% endhighlight %}

## Output on Chrome Console

Here is what we have on console:

![views in backbone js - console output](/wp-content/uploads/2012/12/views-in-backbone-js-console-output.png?fit=690,650)

## Problem in the thought process.

I hope you got an idea. But the problem with this code is defination of render method ie:

{% highlight javascript %}

this.$el.html( this.model.get('name') + ' (' + this.model.get('age') + ') - ' + this.model.get('occupation') );

{% endhighlight %}

As our views get complexed like having images and other things. This will become messy. We are lucky that backbone js has templates for that. So lets head to the new lesson templates in backbone js.

***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
