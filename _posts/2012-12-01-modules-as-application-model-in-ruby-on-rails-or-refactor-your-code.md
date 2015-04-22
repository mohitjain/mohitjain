---
title: Modules as application model in ruby on rails or refactor your code.
author: Mohit Jain
layout: post
comments: true
permalink: /2012/12/modules-as-application-model-in-Ruby on Rails-or-refactor-your-code/

summary: extra_long

categories: optimization performance quick-solution tips-and-tricks utilities
---

Yesterday I was working on [active_admin][1]. This is the first time I am using active admin in any of my project, I find it pretty awesome. If you never used it then [just it a try][2]. So while building dashboard for the active admin. I felt of the need to something like application_model ;) so that the place where I used modules as application model in ruby on rails
I was implementing [highcharts][3] in my application and I want to calculate Daily counts in last 30 days for most of the models likes users, products etc

## Before

So I need this method for lots of models.

 [1]: http://activeadmin.info/ "Active Admin "
 [2]: http://railscasts.com/episodes/284-active-admin "Railcasts for Active admin"
 [3]: http://railscasts.com/episodes/223-charts "HighCharts Railscasts"

{% highlight ruby %}

def self.daily_records_counts_array_in_past_n_days(range = 30.days)
      counts = self.group('Date(created_at)').count
      (range.ago.to_date..Date.today).map {|date| counts[date] || }
   # A method which will return an array of daily new records of users (ie signups) in last 30 days (unless specified)
 end

{% endhighlight %}
Now Same functionality i need for product model and other models too. So instead of copy pasting this method in all the model, we can create a module and include that module in required models.


## After

In lib directory, create a directory ie modules (or name it whatever you want to.)
Now create a file ie act\_as\_countable.rb there and paste this code.

{% highlight ruby %}

module ActAsCountable
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    # define all the class methods here.
    # this method returns total records array in last 30 days. Something like: [10, 40, 70, 90....]
    def total_records_counts_array_in_past_n_days(range = 30.days)
      total_records = []
      counts =  self.group('Date(created_at)').count
      (30.days.ago.to_date..Date.today).each do |day|
        total_records.push(total_records.sum   (counts[day] || ))
      end
      total_records
    end
  # this method returns total daily news records array in last 30 days. Something like: [10, 2, 40, 15....]
    def daily_records_counts_array_in_past_n_days(range = 30.days)
      counts = self.group('Date(created_at)').count
      (range.ago.to_date..Date.today).map {|date| counts[date] || }
    end
  end
end

{% endhighlight %}
Now In Models, where you need these methods. Just include them by:

{% highlight ruby %}
include ActAsCountable
{% endhighlight %}
Once includes you can call these methods as normal class methods like.

{% highlight ruby %}
User.total_records_counts_array_in_past_n_days
Product.total_records_counts_array_in_past_n_days
User.daily_records_counts_array_in_past_n_days(15.days)
Product.daily_records_counts_array_in_past_n_days(15.days)
{% endhighlight %}
If you want to define instance methods in you module. Just define them in the same module like this.
{% highlight ruby %}
module ActAsCountable
  def self.included(base)
    base.extend(ClassMethods)
  end

  module ClassMethods
    def total_records_counts_array_in_past_n_days(range = 30.days)
      total_records = []
      counts =  self.group('Date(created_at)').count
      (30.days.ago.to_date..Date.today).each do |day|
        total_records.push(total_records.sum   (counts[day] || ))
      end
      total_records
    end

    def daily_records_counts_array_in_past_n_days(range = 30.days)
      counts = self.group('Date(created_at)').count
      (range.ago.to_date..Date.today).map {|date| counts[date] || }
    end
  end

  def my_instance_method
    # this is my sample blank instance method
  end
end
{% endhighlight %}
Note: You need to add load these modules via specifying the path in application_controller.rb. Also you need to restart your application.
{% highlight ruby %}
config.autoload_paths  = Dir["#{config.root}/lib/modules/**"]
{% endhighlight %}
You can use module even to refactor the code. For example. Generally my user model has lot of methods related to fetch data from facebook, once user signs up. So create a module for those instance methods.
