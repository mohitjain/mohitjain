---
layout: post
title: Private Class Methods In Ruby
author: Mohit Jain
comments: true
categories: Private Class Methds, Ruby
description: How to define private class methods in ruby
---

A quick tip to how to difine a class method as private method, I have seen lot of people doing it wrong way. Lets take a quick look on how to define a private instance method in ruby

{% highlight ruby %}

class Dog
  def poop
    "Going outside, and will poop :)"
  end

  private

  def bark
    puts 'woof woof'
  end
end

{% endhighlight %}

In the above code, poop is a public method and bark is a private method. If you are calling a public method it will be something like:

{% highlight ruby %}

> dog = Dog.new
> dog.poop
# => "Going outside, and will poop :)"

{% endhighlight %}

But calling a private method will give you an error.

{% highlight ruby %}

> dog = Dog.new
> dog.bark
# NoMethodError: private method `bark' called for #<Dog>

{% endhighlight %}

Now define private class method is not as it is for instance method. They don't exists as normally as instance methods are there but still they exists.

if you want to define a class method private, lets try it the way instance method works,


{% highlight ruby %}

class Dog

  private

  def self.things_can_be_done
    [:bark, :poop, :sleep, :eat]
  end
end

> Dog.things_can_be_done
  # => [:bark, :poop, :sleep, :eat]

{% endhighlight %}

 Oops, private class method has been called :(. This is because the way ruby define the class methods, self is actually Dog and the private method scope was never considered, when ruby was defining this method as class method. Here are couple of ways you can define a class method as private.

## 1. private_class_method

Quick way and easiest way to define a class method as private.

{% highlight ruby %}
class Dog

  def self.things_can_be_done
    [:bark, :poop, :sleep, :eat]
  end

  private_class_method :things_can_be_done
end

> Dog.things_can_be_done
  # => NoMethodError: private method `things_can_be_done' called for Dog:Class

{% endhighlight %}

## 2. class << self

Block of class methods :)

{% highlight ruby %}
class Dog
  class << self
    private

    def things_can_be_done
      [:bark, :poop, :sleep, :eat]
    end
  end
end

> Dog.things_can_be_done
  # => NoMethodError: private method `things_can_be_done' called for Dog:Class
{% endhighlight %}

Good luck ;)
