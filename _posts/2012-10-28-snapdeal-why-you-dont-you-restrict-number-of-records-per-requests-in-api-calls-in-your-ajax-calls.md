---
title: 'Snapdeal &#8211; Why don&#8217;t you restrict number of record per requests in API calls? Visible from ajax calls..!!!'
author: Mohit Jain
layout: post
comments: true
permalink:  /2012/10/snapdeal-why-you-dont-you-restrict-number-of-records-per-requests-in-api-calls-in-your-ajax-calls/
categories: General tips-and-tricks
---
I was working on my project and was testing something via firebug. At the same time I was checking something on [Snapdeal][1] and by mistake opened firebug in Snapdeal tab and just saw the URL of their API in Firebug :)

 [1]: http://www.snapdeal.com "SnapDeal"

 

![snapdeal via firebug](/wp-content/uploads/2012/10/snapdeal-via-firebug.png)

So here is the URL:

    http://www.snapdeal.com/json/product/get/search/64/20/40?q=Type:LED&sort=plrty&keyword=

![SnapDeal Api - Response](/wp-content/uploads/2012/10/Screen-Shot-2012-10-28-at-6.14.51-AM.png)

**and you know the best part**. There is no maximum page size limit in the API, means if I just try to change the number of products in that API call it will hit the database to get that number of goods.

     http://www.snapdeal.com/json/product/get/search/64/20/1000?q=Type:LED&sort=plrty&keyword=

Typical guys have some mercy on your database ;)
