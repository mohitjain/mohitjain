---
title: '6. How to use templates in backbone js &#8211; Learning Backbone js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js optimization
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 6 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

In the previous lessons we learned how to define views and display data, but problem was complex views. In this lesson, we will learn how to use templates in backbone js.

## What we have till now

So from the previous lesson, we have this PersonView:

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
//$(document.body).html(personView.el);  // this is not ideal but good enough for demo.
{% endhighlight %}

## What was the problem

The problem is this code is:

{% highlight javascript %}

this.$el.html( this.model.get('name') + ' (' + this.model.get('age') + ') - ' + this.model.get('occupation') );

{% endhighlight %}

This will go more complicated if we have images or some complex views etc.

## Using a template

Let's use a template, and we pass data to that template, and in return, that template returns the full HTML view. Take a look at this code and let's discuss it line by line.

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

// var person = new Person;
// var personView = new PersonView({ model: person });
//$(document.body).html(personView.el);  // this is not ideal but good enough for demo.

{% endhighlight %}
<!--more-->

So we introduced a new line i.e.,

{% highlight javascript %}
my_template: _.template("<strong><%= name %></strong> (<%= age %>) - <%= occupation %>"),
{% endhighlight %}
Backbone js has a feature that you can define a template using underscore js that we included in lesson 1, and it will compile the template, and then when ever you pass the data, it will return the HTML view as per the code. So in the above line, we defined a template using

{% highlight javascript %}
_.template("<strong><%= name %></strong> (<%= age %>) - <%= occupation %>")
{% endhighlight %}

and we assigned it to

{% highlight javascript %}
my_template = .......
{% endhighlight %}
Now backbone js will compile it and define a function behind the scenes. Next modification that we did was:

{% highlight javascript %}
this.$el.html( this.my_template(this.model.toJSON()));
// it was
//this.$el.html( this.model.get('name') + ' (' + this.model.get('age') + ') - ' + this.model.get('occupation') );
{% endhighlight %}

We called the template and we need to pass the data to that template. We will have access to the model object as we will call:

{% highlight javascript %}
// calls from console
// var person = new Person;
// var personView = new PersonView({ model: person });
{% endhighlight %}

So personView has access to the model, and previously we have seen that toJSON() method just pass the object parameters. Cool. Now let's see the code again and discuss the full flow:

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

{% endhighlight %}

## Fire up the console and fire these commands

{% highlight javascript %}



var person = new Person;  // a person object created...
var personView = new PersonView({ model: person });
personView.el   // ---->; You can call this method and it will display the view..
$(document.body).html(personView.el);  //  --->; This will add output to the dom. This is not ideal but good enough for demo.

{% endhighlight %}

## Whats going on?

*   A personView object is created.
*   Model person has been passed to that personView object.
*   So personView has access to the person object.
*   personView constructor will call render method.
*   render method will call template via my\_template and pass data to my\_template
*   my_template will accepts the parameters and assign proper values and return to render.

Cool :)

## Output on Chrome Console

Now Lets see what chrome developer tools say:

![defining templates in backbone js](/wp-content/uploads/2012/12/defining-templates-in-backbone-js.png?fit=693,520)

The templates we will be defined is known as inline templates. We can improve this code too. Let's see that in the next lesson.


***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself, and I will try to reply back asap.
