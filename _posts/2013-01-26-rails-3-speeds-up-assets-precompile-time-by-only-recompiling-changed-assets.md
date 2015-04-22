---
title: Rails 3 Speeds up assets precompile time by only recompiling changed assets
author: Mohit Jain
layout: post
permalink:  /2013/01/rails-3-speeds-up-assets-precompile-time-by-only-recompiling-changed-assets/



categories: optimization performance quick-solution Server tips-and-tricks
---

Speeds up assets precompile time by only recompiling changed assets, based on a hash of their source files, just by adding a small gem ;)

{% highlight ruby %}

group :assets do
  ...
  gem 'turbo-sprockets-rails3'
end
{% endhighlight %}

Run bundle to install the gem, and you’re done!

Test it out by running rake assets:precompile. When it’s finished, you should see a new file at public/assets/sources_manifest.yml, which includes the source fingerprints for your assets. Go on, run rake assets:precompile again, and it should be a whole lot faster than before.

**Removing Expired Assets**
You can configure the expiry time by setting config.assets.expire_after in config/environments/production.rb. An expiry time of 2 weeks could be configured with the following code:

{% highlight ruby %}
config.assets.expire_after 2.weeks
{% endhighlight %}
This post is basically a short version of readme file of [actual gem][1]. Please check the readme file for more updates.

 [1]: https://github.com/ndbroadbent/turbo-sprockets-rails3
