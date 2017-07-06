---
title: >
  Some basic guidelines I always follow before launching a ruby on rails
  application.
author: Mohit Jain
layout: post
comments: true
permalink:  /2012/12/some-basic-guidelines-i-always-follow-before-launching-an-Ruby on Rails-application/
categories: General optimization performance quick-solution Server tips-and-tricks utilities
---

These are some basic guidelines I always follow before launching a ruby on rails application.

1.  Compress all image with [smusher][1] gem.
2.  Intergrate[ DelayedJob WebView][2] if you are using a Delayed job.
3.  Enable action caching when needed.
4.  Update Read me file of your project. It should be descriptive. Examples: [Delayed Job][3]
5.  Compress js and css
6.  Integrate [Airbrake][4]
7.  Make Sure facebook and twitter or any other social login applications have proper logos, descriptions, etc.
8.  Facebook Login should be in a  pop-up.
9.  Check [Gtmetrics][5] rating and fix them.
10. Integrate [New Relic][6]
11. [Logs files should be rotated][7]
12. Add proper database[ indexes][8].
13. [Configure timezone][9] of your server based on the client requirements.
14. Use [handle_asynchronously][3] in the delayed job for email sending and a lot of other call backs or methods to optimize performance.
15. Store all the data what ever you can.
16. Proper comments should be there.
17. Place google analytics code.
18. Test on all the major browsers which includes Firefox, Chrome, Internet Explorer, Safari
19. S[ave images with interlace][10] if you are using too many images on the website.
20. [Add cache control][11] headers
21. Make sure you have a contact us page
22. If user doesn't come back after three days send him a reminder :) It should be a personal email and take this email seriously

 [1]: http://www.codebeerstartups.com/compress-all-your-public-images-using-smush-it-before-going-to-production-mode/
 [2]: http://www.codebeerstartups.com/delayed-job-web-view/
 [3]: https://github.com/collectiveidea/delayed_job
 [4]: https://airbrake.io/pages/home
 [5]: http://gtmetrix.com/dashboard.html
 [6]: http://newrelic.com/
 [7]: http://www.codebeerstartups.com/rotating-rails-log-files/
 [8]: http://www.codebeerstartups.com/always-add-db-index/
 [9]: http://www.codebeerstartups.com/configure-time-zones-for-your-debian-based-server/
 [10]: http://www.codebeerstartups.com/save-image-as-progressive-image-using-paperclip-and-imagemagick/
 [11]: http://www.codebeerstartups.com/how-to-add-cache-control-expires-headers-to-images-content-served-by-s3/
