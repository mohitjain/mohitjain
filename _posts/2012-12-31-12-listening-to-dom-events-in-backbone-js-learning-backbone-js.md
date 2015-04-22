---
title: '12 Listening to DOM events in backbone js  &#8211; Learning Backbone js'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---


> This entry is part 12 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

So here we are, DOM events in backbone js. I got 8 emails so far requesting for a lesson to understand DOM events in backbone js. To all of them I just replied, I have that thing in my list. Just wait a little and another thing was why you are doing everything on console. I want to something on browser window too. For those folks here is the first episode when we are doing something on browser window. Anyways. Coming back to the lesson. We want to add code for listening to dom events in backbone js. What will be done in this lesson


*   You can see list of people
*   You can click on any person and edit his/her name
*   You can add a new person
*   You can delete a person record.

You can see a [live demo of final outcome here][1].
[1]: http://listen-dom-events-backbone.herokuapp.com/ " Listening to Dom events in backbone js"

## What we have till now

*   We have Person, PersonView, PeopleCollection, PeopleCollectionView
*   App namespace
*   Template a personView
*   We learnt validations, although we are not using that in our sample codes.


I am starting the application with this code and I hope you can understand all of it very easily. If not then checkout the previous lessons.

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


// Person Model
App.Models.Person = Backbone.Model.extend({
	defaults: {
		name: 'Guest User',
		age: 30,
		occupation: 'worker'
	}
});

// A List of People
App.Collections.People = Backbone.Collection.extend({
	model: App.Models.Person
});


// View for all people
App.Views.People = Backbone.View.extend({
	tagName: 'ul',

	render: function(){
		this.collection.each(function(person){
			var personView = new App.Views.Person({ model: person });
			this.$el.append(personView.render().el);
		}, this);

		return this;
	}
});

// The View for a Person
App.Views.Person = Backbone.View.extend({
	tagName: 'li',

	template: template('personTemplate'),


	render: function(){
		this.$el.html( this.template(this.model.toJSON()));
		return this;
	}
});

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

var peopleView = new App.Views.People({ collection: peopleCollection });
$(document.body).append(peopleView.render().el);
})();

{% endhighlight %}

<!--more-->

## Adding a listener for click event

So very first thing that we want to do is: listening to click event on a particular person record. This is simple to do in PersonView *(check inline comments)*

{% highlight javascript %}

// The View for a Person
App.Views.Person = Backbone.View.extend({
	tagName: 'li',
	template: template('personTemplate'),
	// we defined a click event and on any click we can calling a showAlert function
        // which is just displaying a alert box.
	events: {
	 'click' : 'showAlert'

	},

	showAlert: function(){
		alert("You clicked me");
	},

	render: function(){
		this.$el.html( this.template(this.model.toJSON()));
		return this;
	}
});

{% endhighlight %}

Lets move to browser and lets see what happens when we click on a person record.


![12 Listening to Dom events in backbone js](/wp-content/uploads/2012/12/Screen-Shot-2012-12-31-at-7.46.50-PM.png?fit=1015,404)

**A useful tip:**
What if you just want to trigger click only for the name of the person not on age or occupation ie some internal element. Pretty easy..

{% highlight javascript %}

events: {
   'click strong' : 'showAlert'
},

{% endhighlight %}

Ok, so we got the basic idea how to add dom events in our PersonView. We can add all other events like dblclick, mouseover etc.

Lets move ahead and removing all the code we added for click event etc. Lets first modify our template ie personTemplate and add two button edit and delete.

{% highlight javascript %}

<script id="personTemplate" type="text/template">
	<span><strong><%= name %></strong> (<%= age %>) - <%= occupation %></span>
	<button class="edit">Edit</button>
	<button class="delete">Delete</button>
</script>

{% endhighlight %}

Lets head back to console to see what we have.
![12 Listening to Dom events in backbone js](/wp-content/uploads/2012/12/Screen-Shot-2012-12-31-at-7.56.17-PM.png?fit=660,122)


So now we do have two buttons for each row, edit and delete, which don’t do anything but we have them. So now head back to your PersonView and add events for these two one by one.

## Edit Button:

For edit we need to do these things:

*   Get the previous Content
*   Take new user input
*   Update the view with new content

Lets add click events and getting new values.

{% highlight javascript %}
events: {
	 'click .edit' : 'editPerson'
  },

editPerson: function(){
	var newName = prompt("Please enter the new name", this.model.get('name'));
	this.model.set('name', newName);
},

{% endhighlight %}

Trying this on browser.

1.  Loading the page will display three people record
2.  Click on edit and lets update the name of the user using promt
3.  Again call render and append peopleView in dom. ie $(document.body).append(peopleView.render().el);

![Listening to dom events in backbone js](/wp-content/uploads/2012/12/Screen-Shot-2012-12-31-at-8.41.42-PM.png?fit=911,362)



Cool, So now we want whenever we change the name of the person, it should just update the view of that person. We can do this just by binding a function (also known as listeners). So just simply bind onchange event in PersonView like this:

{% highlight javascript %}

initialize: function(){
		this.model.on('change', this.render, this);
},

{% endhighlight %}

So basically we are re-rendering the personView whenever its model is changing. Now hit refresh and try to change the name of the person using prompt. It will just re-render the view automatically :) Cool naa..!!!

But the problem is when you hit cancel.. boom.. Check the code with inline comments…

{% highlight javascript %}

// The View for a Person
App.Views.Person = Backbone.View.extend({
	tagName: 'li',

	template: template('personTemplate'),

	initialize: function(){
		this.model.on('change', this.render, this);
	},

	events: {
	 'click .edit' : 'editPerson'
	},

	editPerson: function(){
		var newName = prompt("Please enter the new name", this.model.get('name'));
		if (!newName)return;  // don't do anything if cancel is pressed..
		this.model.set('name', newName);
	},

	render: function(){
		this.$el.html( this.template(this.model.toJSON()));
		return this;
	}
});

{% endhighlight %}

Another way of doing this can be setting [validations that we learnt in lesson 4 ie validations in models][8]
Also add valdiations by trimming the white spaces etc.

 [8]: http://www.codebeerstartups.com/2012/12/4-adding-validations-in-models-in-backbone-js-learning-backbone-js/ "4. Adding Validations in models in backbone js – Learning Backbone js"

So thats supercool for editing a person name. Now lets move ahead and add a functionality for deleting a record.

## Deleting a record:

1.  Lets first bind a delete click
2.  Now call a destroy method which will destroy the object
3.  Add a listener for destroy
4.  Remove the element from DOM, will be called by listner

Here is the code for that, pretty simple. *(Check inline comments..)*

{% highlight javascript %}

// The View for a Person
App.Views.Person = Backbone.View.extend({
	tagName: 'li',

	template: template('personTemplate'),

	initialize: function(){
		this.model.on('change', this.render, this);
		this.model.on('destroy', this.remove, this); // 3. Adding a destroy announcer..
	},

	events: {
	 'click .edit' : 'editPerson',
	 'click .delete' : 'DestroyPerson'	/// 1. Binding a Destroy for the listing to click event on delete button..
	},

	editPerson: function(){
		var newName = prompt("Please enter the new name", this.model.get('name'));
		if (!newName)return;
		this.model.set('name', newName);
	},

	DestroyPerson: function(){
		this.model.destroy();  // 2. calling backbone js destroy function to destroy that model object
	},

	remove: function(){
		this.$el.remove();  // 4. Calling Jquery remove function to remove that HTML li tag element..
	},

	render: function(){
		this.$el.html( this.template(this.model.toJSON()));
		return this;
	}
});

{% endhighlight %}

I hope are with me without losing the grip of the what happening here.

## Lets do add a new person record.

So lets create a simple form in index.html ie

{% highlight javascript %}

<form id="addPerson" action="">
		<input type="text" placeholder="Name of the person">
		<input type="submit" value="Add Person">
</form>

{% endhighlight %}

Now we need to do these things:

1.  Create a newView for newPerson and Read value from the textbox
2.  Create a new model instance
3.  Add into the collection
4.  Render the new collection

So pretty simple:
Defining a new view for record

{% highlight javascript %}

App.Views.AddPerson = Backbone.View.extend({
	el: '#addPerson',  # referencing the form itself.

	events: {
		'submit': 'submit'  // binding submit click to submit function..
	},

	submit: function(e){
		e.preventDefault();  // preventing default submission..
		var newPersonName = $(e.currentTarget).find('input[type=text]').val();  // getting new form values..
		var person = new App.Models.Person({ name: newPersonName });// creating a new person object..
		this.collection.add(person); // adding this to current collection..

	}
});

{% endhighlight %}

We are adding person to collection to adding listeners for it.

{% highlight javascript %}

// View for all people
App.Views.People = Backbone.View.extend({
	tagName: 'ul',

	initialize: function(){
		this.collection.on('add', this.addOne, this);  // listeners/anouncers for the collection on add..
	},

// refactored render method...
	render: function(){
		this.collection.each(this.addOne, this);
		return this;
	},
// called from render method of collection view..
	addOne: function(person){
		var personView = new App.Views.Person({ model: person });
		this.$el.append(personView.render().el);
	}
});
var addPersonView = new App.Views.AddPerson({ collection: peopleCollection });
peopleView = new App.Views.People({ collection: peopleCollection });
$(document.body).append(peopleView.render().el);

{% endhighlight %}
Hit refresh and now try add, edit and delete. Super Cool ;) Thats all about listening to dom events in backbone js and so called mini project.

***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
