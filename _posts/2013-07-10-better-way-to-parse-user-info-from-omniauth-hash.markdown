---
layout: post
title: "Better way to parse user info from omniauth hash"
description: "How to parse user info from facebook, google omniauth hash in a better way"
date: 2013-07-10 04:06
categories: omniauth facebook ruby ruby-on-rails
---

Let's assume we have to parse this hash. There can be the case we are not getting the keys as a response. So this post is about handling those cases.

{% highlight ruby %}

  auth = {
    :provider => 'facebook',
    :uid => '1234567',
    :info => {
      :nickname => 'jbloggs',
      :email => 'joe@bloggs.com',
      :name => 'Joe Bloggs',
      :first_name => 'Joe',
      :last_name => 'Bloggs',
      :image => 'http://graph.facebook.com/1234567/picture?type=square',
      :urls => { :Facebook => 'http://www.facebook.com/jbloggs' },
      :location => 'Palo Alto, California',
      :verified => true
    },
    :credentials => {
      :token => 'ABCDEF...', # OAuth 2.0 access_token, which you may wish to store
      :expires_at => 1321747205, # when the access token expires (it always will)
      :expires => true # this will always be true
    }
  }

{% endhighlight %}


## General Scenario

So in the best case scenario, we will be having all the keys. So the code like this will work.

{% highlight ruby %}

    user_email = auth[:info][:email]
    user_nickname = auth[:info][:nickname]
    user_location = auth[:info][:location]

{% endhighlight %}

## Exceptional Scenario

Now think about this case when we don't have location key in the response. So we got a hash like this:

{% highlight ruby %}

    auth = {
      :provider => 'facebook',
      :uid => '1234567',
      :info => {
        :nickname => 'jbloggs',
        :email => 'joe@bloggs.com',
        :name => 'Joe Bloggs',
        :first_name => 'Joe',
        :last_name => 'Bloggs',
        :image => 'http://graph.facebook.com/1234567/picture?type=square',
        :urls => { :Facebook => 'http://www.facebook.com/jbloggs' },
        :verified => true
      },
      :credentials => {
        :token => 'ABCDEF...', # OAuth 2.0 access_token, which you may wish to store
        :expires_at => 1321747205, # when the access token expires (it always will)
        :expires => true # this will always be true
      }
    }

{% endhighlight %}




Now in this case

{% highlight ruby %}

  user_email = auth[:info][:email]   # will work
  user_nickname = auth[:info][:nickname] # will work
  user_location = auth[:info][:location] # will return nil here...

{% endhighlight %}


As we all know there is no surety of the hash from the provider so we cant trust it and this 'nil' value can, later on, create issues as we start using it assuming everything is coming perfectly fine from the provider.

So if you want to generate an error in this case when key is not found a simple way can be using statement modifiers ie


{% highlight ruby %}

  auth[:info][:location] or raise ArgumentError
  # => example.rb:23:in `<main>': ArgumentError (ArgumentError)

{% endhighlight %}

but there is a better way ie <strong> using 'fetch' </strong>

{% highlight ruby %}

   auth[:info].fetch(:location) // this will throw an error
   # =>  example.rb:23:in `fetch': key not found: :location (KeyError) from example.rb:23:in `<main>'

{% endhighlight %}

If you are not sure even for info part (which actually you can't be) then you can chain ie like this:

{% highlight ruby %}

  auth.fetch(:info).fetch(:location)

{% endhighlight %}

## Use case 1 - Providing a default value

Now if you want to pass a block for a default value which will be executed if and only if that key is not valuated.

{% highlight ruby %}

  auth[:info].fetch(:location) { "India" }
  # => "India"

{% endhighlight %}

## Use case 2 - Passing a block

Another use case of fetch is it yields the missing key which can be used as

{% highlight ruby %}

  default = ->(key) do
    puts "#{key} is missing "
  end

  auth[:info].fetch(:location, &default)

{% endhighlight %}

## Caution

Another thing to note with fetch is, there is another way to pass the second parameter is method ie:

{% highlight ruby %}

  def default
      "This is my default value"
  end

  auth[:info].fetch(:location, default)

{% endhighlight %}

But the problem with the second one is default method. This method will be computed every time whether your key exists or not, which can be a problem in case you are doing some heavy computation. Using block will execute if and only if the key doesn't exist.

## Fetch also works on arrays

Another thing to note down is fetch also works on array as it works on hash

{% highlight ruby %}

  a = ['a','b','c','d']

  a[10]  # => nil
  a.fetch(10)  # => example.rb:39:in `fetch': index 10 outside of array bounds: -4...4 (IndexError) from example.rb:39:in `<main>'

{% endhighlight %}

That's all :)
