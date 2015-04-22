---
title: Pagination with ajax using will paginate in ruby on rails
author: Mohit Jain
layout: post
comments: true
permalink: /2012/11/pagination-with-ajax-using-will-paginate-in-ruby-on-rails/



categories: optimization quick-solution tips-and-tricks utilities
---

Just learned this trick. Super awesome. You want to enable ajax based pagination with will_paginate within just two mins? Yes.. He is small tip.

I am assuming you have a index page having basic table for now. Here are steps:

*   Make a partial for the value tbody section.
*   Enable format.js in controller
*   Create a file ie index.js.erb. Paste some basic code there.
*   Paste a small code in index.html.erb
*   And its done :)

## Code:

## products_controller

{% highlight ruby %}

def index
  @products = Product.paginate(:order =>"name ASC" ,:page => params[:page], :per_page => 14)
  respond_to do |format|
    format.html # index.html.erb
    format.json { render json: @products }
    format.js
  end
end

{% endhighlight %}
## index.html.erb

{% highlight ruby %}
<h1>Products</h1>
<div id="products">
	<%= render "products/products" %>
</div>
<script>
$(function(){
   $('.pagination a').attr('data-remote', 'true')
});
</script>
{% endhighlight %}


## index.js.erb

{% highlight ruby %}
jQuery('#products').html(" 'products/products' )%>");
$('.pagination a').attr('data-remote', 'true');
{% endhighlight %}
## _products.html.erb

{% highlight ruby %}
<div class="listing">
      <% @products.each do |product| %>
        <div>
	   <span> <%= product.title %> </span>
           <span> <%= product.price %>  </span>
        </div>
     <% end %>
</div>
<%= will_paginate @products %>
{% endhighlight %}
Thats all. So just enabling format.js a partial and some javascript, ajax based pagination is done.
