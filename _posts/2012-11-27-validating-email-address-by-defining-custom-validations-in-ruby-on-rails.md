---
title: Validating email address by defining custom validations in ruby on rails.
author: Mohit Jain
layout: post
permalink:  /2012/11/validating-email-address-by-defining-custom-validations-in-rubyon-rails/



categories: optimization performance quick-solution tips-and-tricks utilities, Validations
---

This post is more about how to define a custom validation in ruby on rails. I am explaining the same by adding a custom validation for email.

**Before:**

{% highlight ruby %}
validates_format_of :email, :with => /A([^@s] )@((?:[-a-z0-9] .)[a-z]{2,})Z/i
{% endhighlight %}
Result we want
**I want to write something like this:**
{% highlight ruby %}
validates :email, :email_format => true
{% endhighlight %}
Here is how to do something like this:

**Step 1:**

Create a new file ie email\_format\_validator.rb in lib directtory and paste following code there:

{% highlight ruby %}

class EmailFormatValidator < ActiveModel::EachValidator
  def validate_each(object, attribute, value)
    unless value =~ /^([^@s] )@((?:[-a-z0-9] .)[a-z]{2,})$/i
      object.errors.add(attribute, :email_format, options)
    end
  end
end

{% endhighlight %}
**Step 2:**

Define error message ie Paste this sample code in config/locales/en.yml

{% highlight ruby %}

# Sample localization file for English. Add more files in this directory for other locales.
# See https://github.com/svenfuchs/rails-i18n/tree/master/rails/locale for starting points.

en:
  hello: "Hello world"
  activerecord:
      errors:
          messages:
              email_format: "is not properly formatted"
{% endhighlight %}
**Step 3:** Auto load validator file ie paste these two lines in application.rb under config directory.

{% highlight ruby %}
config.autoload_paths  = %W(#{config.root}/lib)
config.autoload_paths  = Dir["#{config.root}/lib/**/"]
{% endhighlight %}
Thats it. Now restart your application. Your custom validator is defined :)
