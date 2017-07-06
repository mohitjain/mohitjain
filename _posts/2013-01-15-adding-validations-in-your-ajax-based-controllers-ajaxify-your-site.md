---
title: 'Adding validations in your ajax based controllers &#8211; Ajaxify your site &#8211; Part 2'
author: Mohit Jain
layout: post
comments: true
permalink: /2013/01/adding-validations-in-your-ajax-based-controllers-ajaxify-your-site/
categories: tips-and-tricks utilities
---

A few weeks back I wrote a small blog on how to add Ajax in you forms to Ajaxify your site. If you haven’t checked out that post I will recommend you to check that one [here][1] and check the demo of the application here.

 [1]: http://www.codebeerstartups.com/2012/12/ajaxify-your-site-with-remote-true/

So here are the quick modifications to achieve the basic goal of adding validations. All we need to check is whether product has been saved or not and we can check that just by checking errors count in the product object ie
{% highlight ruby %}
@product.errors.count
{% endhighlight %}
If this counter is zero that means the product has been saved else its not saved. Pretty simple trick ;) So here is the new create.js.erb

{% highlight javascript %}
$('#new_product').remove();
$('#new_product_link').show();
$('#products').append('<%= @product)%>');
$('.new_product').remove();
$('#new_product_link').after('');
{% endhighlight %}

All we are checking is if errors count is the same then-then add new product as row else remove the previous and render the form again and that form will show errors ;)
In the same way, we can add validations for update.js.erb

{% highlight javascript %}

$('#new_product_link').hide().after('');
$('.edit_product').remove();
$('#new_product_link').after('');

{% endhighlight %}
Note: Remember one thing to handle js code in a proper way as there are certain cases when two forms will be displayed. For example: Click on the new product link and now try to edit a product. I hope you can easily handle that case just by adding one or two lines od Jquery code. If you facing any issues then do let me know. You can find complete source code [here][2] and also see a demo [here][3].

 [2]: https://github.com/mohitjain/ajaxified_scaffold "Source code for Ajaxified Scaffold"
 [3]: http://ajaxified-scaffold.herokuapp.com/
