---
layout: post
title: "How to optimize Active Record Queries"
description: How to optimize Active Record Queries in ruby on rails
date: 2013-04-15 02:19
categories: performance mysql  active-record
---
Using the select parameter in Active Record association, you can speed up your application about 50% and more.

##Before

{% highlight ruby %}

class Patient < ActiveRecord::Base
  belongs_to :physician
end
class Physician < ActiveRecord::Base
  has_many :patients
end

{% endhighlight %}

<!--more-->

##After

{% highlight ruby %}

class Patient < ActiveRecord::Base
  belongs_to :physician, :select => 'id,name, surname'
end

class Physician < ActiveRecord::Base
  has_many :patients, :select => 'id,name, physician_id'
end

{% endhighlight %}

If you populate a database with some 10000 records each. Results show that it will reduce time up to 50% with respect to fetching all the records.

## Before refactoring:

{% highlight ruby %}

Physician Load (33.9ms)  SELECT `physicians`.* FROM `physicians`
Patient Load (66.5ms)  SELECT `patients`.* FROM `patients` WHERE `patients`.`physician_id` IN (1, 2, 3,...)

{% endhighlight %}

## After refactoring:

{% highlight ruby %}

Physician Load (31.8ms)  SELECT `physicians`.* FROM `physicians`
Patient Load (22.3ms)  SELECT name,physician_id,id FROM `patients` WHERE `patients`.`physician_id` IN (1, 2, 3,...)

{% endhighlight %}

Pulling all the columns from doesn't make any sense. So pull only those columns which we actually need. If you need to specify things in respective queries then do it.
