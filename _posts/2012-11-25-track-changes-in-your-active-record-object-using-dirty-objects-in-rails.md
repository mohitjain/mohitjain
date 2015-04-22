---
title: Track changes in your active record object using Dirty Objects in Rails
author: Mohit Jain
layout: post
permalink:  /2012/11/track-changes-in-your-active-record-object-using-dirty-objects-in-rails/



categories: optimization performance quick-solution tips-and-tricks
---

If you want to track whether your active record objects have been modified or not. It becomes a lot easier with the dirty object functionality. Its pretty simple and clean.

{% highlight ruby %}

article = Article.first
article.changed?  #=> false

# Track changes to individual attributes with# attr_name_changed? accessor
article.title  #=> "Title"
article.title = "New Title"
article.title_changed? #=> true

# Access previous value with attr_name_was accessor
article.title_was  #=> "Title"

# See both previous and current value with attr_name_change accessor
article.title_change  #=> ["Title", "New Title"]

{% endhighlight %}
You can also query to object directly for its list of all changed attributes.

{% highlight ruby %}

# Get a list of changed attributes
article.changed  #=> ['title']
# Get the hash of changed attributes and their previous and current values
article.changes  #=> { 'title' => ["Title", "New Title"] }
{% endhighlight %}
Once you save a dirty object it clears out its changed state tracking and is once again considered unchanged.

{% highlight ruby %}
article.changed?  #=> true
article.save  #=> truearticle.changed?  #=> false
{% endhighlight %}
If you’re going to be modifying an attribute outside of the attr= writer, you can use attr\_name\_will_change! to tell the object to be aware of the change:

{% highlight ruby %}
article = Article.first
article.title_will_change!
article.title.upcase!
article.title_change  #=> ['Title', 'TITLE']
{% endhighlight %}
