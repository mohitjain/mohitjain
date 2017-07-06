---
title: 'validates_uniqueness_of doesn&#8217;t guarantee the absence of duplicate record insertions'
author: Mohit Jain
layout: post
comments: true
permalink:  /2012/11/validates_uniqueness_of-doesnt-guarantee-the-absence-of-duplicate-record-insertions/
categories: validations
---
From the title this post you may say, What the crap? validates\_uniqueness\_of is the inbuilt functionality of ruby on rails. But yes it's true. I just came to know about this today when I saw some duplicate records in my project database.

Here is the what official guide says:

*Using this validation method in conjunction with ActiveRecord::Validations#save does not guarantee the absence of duplicate record insertions because uniqueness checks on the application level are inherently prone to race conditions. For example, suppose that two users try to post a Comment at the same time, and a Comment’s title must be unique. At the database level, the actions performed by these users could be interleaved in the following manner:*

![Concurrency and integrity with validates_presence_of](/wp-content/uploads/2012/11/validates_uniqueness_of-.png?fit=554,43)

This could even happen if you use transactions with the ‘serializable’ isolation level. The best way to work around this problem is to add a unique index to the database table using ActiveRecord::ConnectionAdapters::SchemaStatements#add_index. In the rare case that a race condition occurs, the database will guarantee the field’s uniqueness.


Here is the solution always add the unique index in the database. For example for your application you can do something like:

{% highlight ruby %}
add_index :posts, :title, :unique => true
{% endhighlight %}
For all future migrations or model creation migrations etc. Do this

{% highlight ruby %}
create_table :posts do |t|
    t.string :title, :unqiue => true
    t.text :description
    t.timestamps
end
{% endhighlight %}
Source: [http://api.rubyonrails.org/classes/ActiveRecord/Validations/ClassMethods.html#method-i-validates\_uniqueness\_of][3]

 [3]: http://api.rubyonrails.org/classes/ActiveRecord/Validations/ClassMethods.html#method-i-validates_uniqueness_of "http://api.rubyonrails.org/classes/ActiveRecord/Validations/ClassMethods.html#method-i-validates_uniqueness_of"
