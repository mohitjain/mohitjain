---
layout: post
title: "Keeping ruby on rails model DRY - MetaProgramming"
keywords: metaprogramming, ruby,  DRY models
date: 2013-04-28 17:41
categories: metaprogramming
---

If you find some methods whose definitions are more or less similar, only different by the method name, it may use meta programming to simplify the things to make your model more clean and DRY.

Consider this simple example where we have an article with three states.



## Before

{% highlight ruby %}

  class Article < ActiveRecord::Base

    def self.all_published
      where("state = ?", "published")
    end

    def self.all_draft
      where("state = ?", "draft")
    end

    def self.all_spam
       where("state = ?", "spam")
    end

    def published?
      self.state == 'published'
    end

    def draft?
      self.state == 'draft'
    end

    def spam?
      self.state == 'spam'
    end
  end

{% endhighlight %}

Now this code can be written as:

## After

{% highlight ruby %}

  class Article < ActiveRecord::Base

    STATES = ['draft', 'published', 'spam']

    class <<self
      STATES.each do |state_name|
        define_method "all_#{state_name}" do
          where("state = ?", state_name)
        end
      end
    end

    STATES.each do |state_name|
      define_method "#{state_name}?" do
        self.state == state_name
      end
    end

  end

{% endhighlight %}

This makes your code drier and cleaner. And adding more states makes it easier to modify.
