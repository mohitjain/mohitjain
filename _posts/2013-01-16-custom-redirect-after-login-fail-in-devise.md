---
title: Custom redirect after login fail in devise
author: Mohit Jain
layout: post
permalink: /2013/01/custom-redirect-after-login-fail-in-devise/



categories: quick-solution tips-and-tricks
---

Last weekend had a small hackathon in our office and we build a [simple group emailing service][1] and in that project we need to make some overrides in devise and one of them was custom redirect in case login fails.

 [1]: http://emaillist.io?utm_source=codebeerstartups&utm_medium=blogpost&utm_campaign=codebeerstartups "Group Emailing service"

By default when the login fails it redirects to “users/sign_in”. Here is how you can over ride this.

1. Create a custom_failure.rb in your lib directory, with:

{% highlight ruby %}

class CustomFailure < Devise::FailureApp
  def redirect_url
    your_path
  end
  def respond
    if http_auth?
      http_auth
    else
      redirect
    end
  end
end
{% endhighlight %}

2. In you Devise initializer, include:

{% highlight ruby %}
config.warden do |manager|
  manager.failure_app = CustomFailure
end
{% endhighlight %}

3. Make sure Rails is loadin your lib files, in your application.rb :

{% highlight ruby %}
config.autoload_paths  = %W(#{config.root}/lib)
{% endhighlight %}

4. Don’t forget to restart your server.

Thats a way to handle custom redirect after login fail in devise. Please feel free to embarrass me with your improvements in the comments.
