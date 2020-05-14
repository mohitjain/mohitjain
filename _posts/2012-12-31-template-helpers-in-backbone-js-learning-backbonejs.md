---
title: 'Template helpers in backbone js - Learning BackboneJs'
author: Mohit Jain
layout: post
comments: true
categories: Backbone.js optimization
banner_image: "/media/backbone.jpg"
featured: true
---

> This entry is part 10 of 14 in the series for [A Complete Guide for Learning Backbone Js](/a-complete-guide-for-learning-backbone-js/)

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

# Agenda

Templates make your code look more neat and clean and helps in a lot of other ways.

# Template helpers

So far we are using embedded templates in our HTML file ie

{% highlight javascript %}

  <script id="personTemplate" type="text/template">
      <strong><%= name %></strong> (<%= age %>) - <%= occupation %>
  </script>

{% endhighlight %}

In our view we are calling this template like this:

{% highlight javascript %}

  template: _.template( $('#personTemplate').html()),

{% endhighlight %}

One good thing over here is we can define a template helpers in backbone js (as a global function) and optimize our code like this.

{% highlight javascript %}

  var template = function(id){
      return _.template( $('#' + id).html() );
  };

{% endhighlight %}

Now in personView call the template by just calling:

{% highlight javascript %}

  template: template('personTemplate'),

{% endhighlight %}

Just defining a simple function can make our life much easier as we have to call many templates in real our applications. That's all for this lesson. Will come back soon with an important topic ie namespacing.


***

## Source code

If you are facing any issues. Check out the source code files at [github](https://github.com/mohitjain/learning_basics_backbone "Source Code for the post"). I will be creating more and more directories in the same repo regarding each post. Still, if you have any doubts you can comment on the blog post itself and I will try to reply back asap.
