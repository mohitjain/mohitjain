---
title: 'Ajaxify your site with remote => true and respond_to block'
author: Mohit Jain
layout: post
permalink: /2012/12/ajaxify-your-site-with-remote-true/



categories: tips-and-tricks utilities
---

Here is a small application which is basically a scaffold but create, edit, update and destroy are done using ajax ie remote => true option in rails. [See Demo.][1]

 [1]: http://ajaxified-scaffold.herokuapp.com/ "Demo of the application"

So the very first thing is understand repond_to block. If you run a scaffold command and see new action code it looks like:

{% highlight ruby %}

# GET /products/new
  # GET /products/new.json
  def new
    @product = Product.new

    respond_to do |format|
      format.html # new.html.erb
      format.json { render json: @product }
    end
  end

{% endhighlight %}

[which basically means this will respond to only two kind of request one is html and second is json.][2]

 [2]: http://api.rubyonrails.org/classes/ActionController/MimeResponds/ClassMethods.html#method-i-respond_to "Rails api doc for repond_to block"

Now for your your ajax request your need to tell controller to respond to js request which can be done but adding a line ie.
{% highlight ruby %}

# GET /products/new
  # GET /products/new.json
  # GET /products/new.js
  def new
    @product = Product.new

    respond_to do |format|
      format.html # new.html.erb
      format.json { render json: @product }
      format.js
    end
  end

{% endhighlight %}

Now you have told controller to send response for js request. Create a file ie new.js.erb. This is the file where you write some js code to make the response to do the desired stuff.

Cool. Lets start from scratch.

**Step 1:** Make a new application
**Step 2:** Generate a scaffold
**Step 3:** Start making the js requests and add some code to get desired results.

Create an application and generate a scaffold ie:

{% highlight ruby %}
rails g scaffold products name:string price:integer
{% endhighlight %}
Once You have it. Make a js requests for new link from index.html.erb ie:

{% highlight ruby %}
<%= link_to 'New Product', new_product_path, :remote => true, :id => "new_product_link" %>
{% endhighlight %}
Now enable js requests in the controller for new action ie:

{% highlight ruby %}
# GET /products/new
  # GET /products/new.json
  def new
    @product = Product.new

    respond_to do |format|
      format.html # new.html.erb
      format.json { render json: @product }
      format.js
    end
  end
{% endhighlight %}
Now create a new.js.erb file in products directory and add this line of code:

{% highlight javascript %}
$('#new_product_link').hide().after('');
{% endhighlight %}
This will hide the new\_product\_link and add a new product form. Hit refresh of you index page and try to click on new product link. ;)

Now if you try to submit the form, it will be submitted as normal form. To make it ajax. Modify the form like this:

{% highlight ruby %}
<%= form_for @product, :remote => true do |f| %> # adding remote=> true to form.
{% endhighlight %}
Now refresh and try to submit the form. Form will be submitted but request is not handled properly on controller end. Here is the same code for create action.

{% highlight ruby %}
# POST /products
# POST /products.json
def create
  @product = Product.new(params[:product])

  respond_to do |format|
    if @product.save
      format.html { redirect_to @product, notice: 'Product was successfully created.' }
      format.json { render json: @product, status: :created, location: @product }
      format.js
    else
      format.html { render action: "new" }
      format.json { render json: @product.errors, status: :unprocessable_entity }
      format.js
    end
  end
end
{% endhighlight %}
<!--more-->


and create.js.erb

{% highlight javascript %}
$('#new_product').remove();
$('#new_product_link').show();
$('#products').append(' @product)%>');
{% endhighlight %}
Hey hey.. Before you try to submit the form. Modify your index.html.erb like this so that you can render a product row in index.html.erb.

{% highlight html %}
<h1>Listing products</h1>
<table>
  <tr>
    <th>Name</th>
    <th>Price</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>
  <tbody id="products">
<% @products.each do |product| %>
<%= render "product", :product => product %>
<% end %>
</tbody>
</table>
<br />
<%= link_to 'New Product', new_product_path, :remote => true, :id => "new_product_link" %>
{% endhighlight %}
and a product.html.erb partial ie _product.html.erb

{% highlight html %}
<tr id="product_<%= product.id %>">
  <td><%= product.name %></td>
  <td><%= product.price %></td>
  <td><%= link_to 'Show', product %></td>
  <td><%= link_to 'Edit', edit_product_path(product) %></td>
  <td><%= link_to 'Destroy', product, method: :delete, data: { confirm: 'Are you sure?' } %></td>
</tr>
{% endhighlight %}

Once you make this modifications. You can see that redering a new form and create a new product is completely ajaxified. In the same way you can do for edit form and update and for destroy.

[Source code: Clone this repo to see the whole code][3]

 [3]: https://github.com/mohitjain/ajaxified_scaffold "Source code for Ajaxified Scaffold"

This is how you can a lot of things to ajaxify your site with respond_to and remote => true.

**Update:**

[Do checkout how to add validations in ajax based forms][4]

[4]: http://www.codebeerstartups.com/2013/01/adding-validations-in-your-ajax-based-controllers-ajaxify-your-site  "Adding validations in your ajax based controllers – Ajaxify your site – Part 2"
