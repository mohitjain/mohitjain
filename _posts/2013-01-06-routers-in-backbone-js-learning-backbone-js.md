---
title: '13 Routers in backbone js &#8211; Learning backbone js'
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/routers-in-backbone-js-learning-backbone-js/
categories: Backbone.js
banner_image: "/media/backbone.jpg"
featured: true
---


> This entry is part 13 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

So here we are back on backbone js. I got lot of feedback emails from the readers telling me how much they are loving the series. Thanks to all of them.

Ok. In this lesson we will learning routers in backbone js. Routing is pretty awesome in backbone js, if you are ruby on rails developer you will find it pretty simpler to that you are doing in ruby on rails.

## What we have till now

Lets start from a bare bone code ie:

{% highlight javascript %}

(function(){

  window.App = {
  	Models: {},
  	Collections: {},
  	Views: {},
  	Router: {}
  };

})();

{% endhighlight %}

## Defining a router

A simple Name spaced model, collection, views and a new one router. So lets define a router ie:

{% highlight javascript %}

App.Router = Backbone.Router.extend({

});

{% endhighlight %}

## Defining a root route

Now just for simplicity lets add a root route ie when page has been loaded..

{% highlight javascript %}

App.Router = Backbone.Router.extend({
	routes: {
		'': 'index'
	},

	index: function(){
		$(document.body).append("Index route has been called..");
	}

});

{% endhighlight %}

<!--more-->

So now we need to initiate the router and one thing we need to do is: Enabling backbone history so that backbone start monitoring hash changes in url.

{% highlight javascript %}

(function(){

window.App = {
	Models: {},
	Collections: {},
	Views: {},
	Router: {}
};
App.Router = Backbone.Router.extend({
	routes: {
		'': 'index'
	},
	index: function(){
		$(document.body).append("Index route has been called..");
	}
});

new App.Router;
Backbone.history.start();

})();

{% endhighlight %}

So if we open index.html in browser we will see a string as specified in the browser. Something like this. (Please make sure you check url from the screenshot ie file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html )

![routes in backbone js 1](/wp-content/uploads/2013/01/routes-in-backbone-js-1.png?fit=733,229)


## Adding a hash tag route

Ok lets move ahead and add a route for hash tag.

{% highlight javascript %}

App.Router = Backbone.Router.extend({
	routes: {
		'': 'index',
		'show': 'show'
	},

	index: function(){
		$(document.body).append("Index route has been called..");
	},

	show: function(){
		$(document.body).append("Show route has been called..");
	},

});

{% endhighlight %}

So if we open index.html in browser we will see a string as specified in the browser. Something like this. (Please make sure you check url from the screenshot ie

     file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html#show )


![routes in backbone js 2](/wp-content/uploads/2013/01/routes-in-backbone-js-21.png?fit=758,155)

Ok Lets add a better route for show. Think about this. You want to say show/1 or show/2 or show/3 and based upon the number you want to display something. Here is how you can do something like that..

## Passing a param in the route

{% highlight javascript %}

App.Router = Backbone.Router.extend({
	routes: {
		'': 'index',
		'show/:id': 'show'
	},

	index: function(){
		$(document.body).append("Index route has been called..");
	},

	show: function(id){
		$(document.body).append("Show route has been called.. with id equals : "   id);
	},

});

{% endhighlight %}

So if we open index.html in browser we will see a string as specified in the browser. Something like this. (Please make sure you check url from the screenshot ie

    file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html#show/3 )


![routes in backbone js 3](/wp-content/uploads/2013/01/routes-in-backbone-js-3.png?fit=894,214)

Ok if I want to specify something like: #download/3/12/23 in this case the above id routes will not work. So to handle that, take a look on this..

{% highlight javascript %}

App.Router = Backbone.Router.extend({
	routes: {
		'': 'index',
		'show/:id': 'show',
		'download/*random': 'download'
	},

	index: function(){
		$(document.body).append("Index route has been called..");
	},

	show: function(id){
		$(document.body).append("Show route has been called.. with id equals : "   id);
	},

	download: function(random){
		$(document.body).append("download route has been called.. with random equals : "   random);
	}

});
{% endhighlight %}

So if we open index.html in browser we will see a string as specified in the browser. Something like this. (Please make sure you check url from the screenshot ie

{% highlight javascript %}

    file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html#download/3/12/23 )
{% endhighlight %}

![routes in backbone js 4](/wp-content/uploads/2013/01/routes-in-backbone-js-4.png?fit=866,148)

Another usefull route that I feel most of the application need is for search and last is default route in case nothing is specified that one will be called..

{% highlight javascript %}

App.Router = Backbone.Router.extend({
	routes: {
		'': 'index',
		'show/:id': 'show',
		'download/*random': 'download',
		'search/:query': 'search',
		'*default': 'default'
	},

	index: function(){
		$(document.body).append("Index route has been called..");
	},

	show: function(id){
		$(document.body).append("Show route has been called.. with id equals : "   id);
	},

	download: function(random){
		$(document.body).append("download route has been called.. with random equals : "   random);
	},

	search: function(query){
		$(document.body).append("Search route has been called.. with query equals : "   query);
	},

	default: function(default){
		$(document.body).append("This route is not hanled.. you tried to access: "   default);

	}

});

{% endhighlight %}

You can try this for search url ie:

{% highlight javascript %}

file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html#search/my_query

{% endhighlight %}

and to check default route here is one example..

{% highlight javascript %}

file://localhost/Users/mohit/projects/codebeerstartups/routes\_in\_backbonejs/index.html#junk

{% endhighlight %}

Thats all for this lesson ie routers in backbone js.

***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
