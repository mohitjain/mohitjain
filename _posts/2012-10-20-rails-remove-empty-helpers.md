---
title: Rails Remove empty helpers
layout: post
comments: true
permalink: /2012/10/rails-remove-empty-helpers/
description: Quick way to remove all empty helpers in ruby on rails.
keywords:  optimizations, cleanup
categories: optimization ruby-on-rails
---
If you use rails generator to create scaffolds or controllers, it will also create some helpers, most of the helpers are useless, just remove them.

Rails provide handy generators to create scaffolds, models, controllers, and views when generating the scaffolds or controllers, it also creates some helpers, some of the helpers may use, but I bet most of the helpers in your project are empty.

Helpers are right places to add the helper method for view pages, but if you don’t need them, why you push these empty helpers to the repository. Although your helpers are empty, rails still take time to load them, Test::Unit or RSpec still load them to run tests.

So I recommend you to remove all the empty helpers from your project, the following is a script to detect empty helpers, remove them and corresponding unit tests or Rspecs.

{% highlight ruby %}
Dir.glob("app/helpers/**/*.rb").each do |file|
  if !File.read(file).index('def')
    FileUtils.rm file

    FileUtils.rm_f file.sub("app/", "test/unit/").sub(".rb", "_test.rb")if File.exists?("test")
    FileUtils.rm_f file.sub("app/", "spec/").sub(".rb", "_spec.rb")if File.exist?("spec")
  end
end
{% endhighlight %}
In rails 3, you can ask rails do not generate helper automatically.
{% highlight ruby %}
config.generators.helper = false
{% endhighlight %}
It’s the only bonus for rails3, it seems there’s no way for rails2.
