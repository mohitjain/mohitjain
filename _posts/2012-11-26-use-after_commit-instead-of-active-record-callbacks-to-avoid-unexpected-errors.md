---
title: Use after_commit instead of active record callbacks to avoid unexpected errors
author: Mohit Jain
layout: post
comments: true
categories: optimization performance quick-solution Server tips-and-tricks
---
AR callbacks after\_create/after\_update/after_destroy to generate background job etc. are useful, but these callbacks are still wrapped in the database transaction, and you may probably get unexpected errors on production servers.

## Before
It’s common to generate a background job to send emails like

{% highlight ruby %}

  class Comment < ActiveRecord::Base
    after_create :asyns_send_notification
    def async_send_notification
      Notifier.send_new_comment_notification(self).deliver
    end
   handle_asynchronously :async_send_notification
  end

  # It looks beautiful that comment record passed to the delayed job and then delayed job will fetch this
  #comment and then post on which this comment has been made and a notification will
  #send via email to the author of that post. Right?

{% endhighlight %}

You won’t see any issue in development, as local DB can commit fast. But in production server, db traffic might be massive, worker probably finish faster than transaction commit. e.g


1. primary process
2. worker process
3. BEGIN

{% highlight ruby %}

  INSERT comment in comments table
  # return id 10 for newly-created notification
  SELECT * FROM notifications WHERE id = 10
  COMMIT

{% endhighlight %}

In this case, the worker process query the newly-created notification before the main process commits the transaction, it will raise NotFoundError, because transaction in worker process can’t read free information from the transaction in the main process.

## Refactor

So we should tell ActiveRecord to generate notification worker after notification insertion transaction committed.

{% highlight ruby %}

  class Comment < ActiveRecord::Base
    after_commit :asyns_send_notification,:on => :create  # This is the main point of the whole thing.

    def async_send_notification
      Notifier.send_new_comment_notification(self).deliver
    end
    handle_asynchronously :async_send_notification
  end

{% endhighlight %}

Now the transactions order becomes

1. main process
2. worker process
3. BEGIN

{% highlight ruby %}

  INSERT comment into comments_table
  return id 10 for newly-created notification
  COMMIT
  SELECT * FROM notifications WHERE id = 10

{% endhighlight %}

Worker process won’t receive NotFoundErrors anymore. :)
