---
title: '10. Template helpers in backbone js &#8211; Learning BackboneJs'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js optimization
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 10 of 14 in the series for [A Complete Guide for Learning Backbone Js](/2012/12/a-complete-guide-for-learning-backbone-js/)

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

# Agenda

Templates make your code look more neat and clean and helps in lot of other ways.

# Template helpers

So far we are using embeeded templates in our html file ie

{% highlight javascript %}

<script id="personTemplate" type="text/template">
	<strong><%= name %></strong> (<%= age %>) - <%= occupation %>
</script>

{% endhighlight %}

In our view we are calling this template like this:

{% highlight javascript %}

template: _.template( $('#personTemplate').html()),

{% endhighlight %}

One good thing over here is we can define a template helpers in backbone js (as a global function) and optimise our code like this.

{% highlight javascript %}

var template = function(id){
	return _.template( $('#' + id).html() );
};

{% endhighlight %}

Now in personView call the template by just calling:

{% highlight javascript %}

template: template('personTemplate'),

{% endhighlight %}

Just defining a simple function can make our life much more easier as we have to call many templates in real our applications. Thats all for this lesson. Will come back soon with a important topic ie name spacing.


***

## Source code

If you are facing any issues. Checkout the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
