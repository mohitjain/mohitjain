---
title: A simple way to implement soft delete in rails application.
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/a-simple-way-to-implement-soft-delete-in-rails-application/



categories: optimization performance quick-solution tips-and-tricks utilities
---

PS: This blog post use modules. If you are not familar with modules in rails application then I will recommend you to check [Modules in ruby on rails ][1]

 [1]: http://www.codebeerstartups.com/modules-as-application-model-in-Ruby on Rails-or-refactor-your-code/ "Modules in ruby on rails."

Here is a simple way to implement soft delete in rails application.
Define two modules Achiver and a module Archivable

{% highlight ruby %}

module Archivable
  def archive!
    self.archive = 1
    self.deleted_at = Time.now
    self.save
  end
end

module Archiver
  def destroy
    self.archive = 1
    self.deleted_at = Time.now
    archive_models!
    self.save
    freeze
  end

  def archive_models!
    archivable_models.each do |model|
      model_name = model.name.pluralize.downcase.to_s
      self.send(model_name).each { |m| m.archive! }
    end
  end

  def archivable_models
    ActiveRecord::Base.send(:subclasses).select { |m| m.method_defined?(:archive!)}
  end
end

{% endhighlight %}

Now use these two modules in your models.

{% highlight ruby %}

class Image < ActiveRecord::Base
  include Archivable
  belongs_to :user, :counter_cache => true
end

class User < ActiveRecord::Base
  include Archiver
  has_many :images,:order => "created_at DESC", :conditions => "archive = 0", :dependent => :destroy
  attr_accessible :name
end

{% endhighlight %}

This is a **pretty** hack-ish implementation, but it works.
