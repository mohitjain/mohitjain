---
title: 'How to make &#8211;no-ri &#8211;no-rdoc the default for gem install?'
author: Mohit Jain
layout: post
categories: optimization quick-solution tips-and-tricks
---

Most of the people don’t use RI or RDoc from the gems they install in my machine, but every gem you install comes with RI and RDoc by default and we all forget to set –no-ri –no-rdoc while installation. To avoid this for ever just add these two lines to your \`~/.gemrc\` or \`/etc/gemrc\`:

{% highlight ruby %}
install: --no-rdoc --no-ri
update:  --no-rdoc --no-ri
{% endhighlight %}
