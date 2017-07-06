---
title: How to deploy assets on Amazon S3 and why deploying assets to Amazon S3 is important.
author: Mohit Jain
layout: post
comments: true
permalink:  /2012/10/how-to-deploy-assets-on-amazon-s3-and-why-deploying-assets-to-amazon-s3-is-important/
categories: Performance ruby-on-rails
---

I was working on my project [Kwaab][1] and suddenly because of massive traffic (150-200 hits per second), the site starts slowing down. Page load time was increased from 10 seconds to 40 seconds and sometimes even more than that. We tried to increase the server, still no significant improvements. Here are some things we have already done:

 [1]: http://www.kwaab.com/

*   Landing Page is cached
*   2GB of RAM and only 800MB is used
*   CPU utilization is less than 40%
*   User uploaded images are already coming from Amazon s3
*   Use cache control and expiry headers
*   Compress images using smusher
*   Compress js and CSS and lot more basic things we should do.

But still, the site is super damn slow, because the issue was loading time for assets. As my assets were coming from Linode itself and due to high traffic of the website, the client was waiting for assets for like 15 seconds just for the logo, etc., and that was slowing my site.

I got a life saver i.e. [asset_sync][2] a gem to deploy your assets on Amazon bucket :)

 [2]: https://github.com/rumblelabs/asset_sync

##How to implement deploying assets on amazon s3



*   Install the gem:
    If you want, you can put it within your :assets group in your Gemfile.

{% highlight ruby %}

gem "asset_sync"

{% endhighlight %}
*   Create a file asset_sync.yml in your config directory or check out the inbuilt generator i.e

{% highlight ruby %}

rails g asset_sync:install --use-yml --provider=AWS

{% endhighlight %}
    which will generate a file in app/config/asset_sync.yml

    Now I have this asset_sync.yml file, but you can configure it as per the docs of the gems.

{% highlight ruby %}

staging:
  fog_provider: AWS
  aws_access_key_id: **********************
  aws_secret_access_key: **********************
  fog_directory: assetsstaging
  gzip_compression: 'true'
  existing_remote_files: keep

production:
  fog_provider: AWS
  aws_access_key_id: **********************
  aws_secret_access_key: **********************
  fog_directory: assetsproduction
  gzip_compression: 'true'
  existing_remote_files: keep

{% endhighlight %}
*   Place these lines of code in your production/staging environment file:

{% highlight ruby %}
asset_sync_config_file = File.join(Rails.root, 'config', 'asset_sync.yml')
  ASSETCONFIG = HashWithIndifferentAccess.new(YAML::load(IO.read(asset_sync_config_file)))[Rails.env]
  ASSETCONFIG.each do |k,v|
    ENV[k.upcase] ||= v
  end
{% endhighlight %}
*   Down the above code. Place these lines of code which will tell rails to get the assets from here.

{% highlight ruby %}
config.action_controller.asset_host = "//#{ENV['FOG_DIRECTORY']}.s3.amazonaws.com"
{% endhighlight %}
*   Also make sure your production/staging environment files have:

    *   config.assets.digest is set to true.
    *   config.assets.enabled is set to true.

That's it. Now just deploy your Rails application and all the assets will be pushed to the respective bucket on Amazon :) and it solved my server issue to with a considerable amount. We made some more tweaks. I will post them soon.
***PS: In my case, I need to create that Amazon bucket manually. You may need to do so.***
