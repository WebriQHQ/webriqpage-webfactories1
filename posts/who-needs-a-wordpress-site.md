---
title: Who needs a Wordpress Site
shortdesc: Until recently the answer to that question would have been almost everybody. Now the answer to that question is almost nobody.  Why is that?
cmsUserSlug: ""
date: 2016-02-24T16:00:00.000Z
banner: /img/uploads/who-needs-a-wordpress-site.jpg
categories: recent-blog
writer: Philippe Bodart
---

A couple of years ago the answer was most likely everybody, now the answer is almost nobody. Why is that?

### When Static Was It

The first ever website, Tim Berners-Lee’s original home page for the World Wide Web, was static. A website back then was a folder of HTML documents that consisted of just 18 tags. Browsers were simple document navigators that would fetch HTML from a server and allow the end user to navigate them by following hyperlinks. The web was fundamentally static.

As browsers evolved, so did HTML, and gradually the limitations of purely static websites started to show.

The most mainstream answer to the limitations of Static Websites was the LAMP stack and CMS’ such as WordPress, Drupal and Joomla. All of these played an incredibly important role in moving the web forward, enabling the Web 2.0 phenomenon, in which user-generated content became a driving factor for a lot of websites. Users went from following hyperlinks to ordering products, participating in communities and creating content.

### Dynamic Website Wordpress Problems

The dynamic website architecture moved the web forward, but it also opened a can of worms. By a conservative estimate, more than 70% of today’s WordPress installations are vulnerable to known exploits (and WordPress powers more than 23% of the web). Just a few months ago, 12 million Drupal sites needed emergency patching, and any not patched within 7 hours of the exploits’ announcement should be considered infected with malware.. Not a week goes by when I don’t follow a link from social media to a website that shows a “Database connection error.” Scaling a dynamic website can be very expensive, and agencies that launch a campaign website or the like often have to overprovision drastically in order to guard against the website blowing up if it manages to go viral — or else they have to desperately scale it while trying to get it back online (something that never seems to happen during office hours).

We pay a huge price for the underlying complexity of dynamic code running on a server for every request — a price we could avoid paying entirely when this kind of complexity is not needed.

### Is Static the next big thing again and why now?

Why is static website technology taking off now, and why did the early generators fail to make a dent in WordPress’ dominance? What’s changed? And how far can we take this?

Today’s static website tools play into a totally different ecosystem than their predecessors. Many of the constraints that made dynamic websites the best option for creating anything but the most basic online brochure have fallen away. 

### THE BROWSER IS GROWING UP

When Tim Berners-Lee launched the first website of the World Wide Web, a browser was a simple document viewer that could display hypertext, links and little else.

Today, we’re finally in the process of burying the last browser that has been holding the web back (RIP Internet Explorer 8). The modern browser is an operating system in its own right, no longer merely displaying documents downloaded from the web, but capable of running full-fledged web applications, making external calls to API, storing data locally, opening WebSockets to streaming servers, and even handling peer-to-peer connections to other browsers via WebRTC.

With the maturation of browsers, many features that used to require dynamic code running on a server can be moved entirely to the client. Want comments on your website? Add Disqus, Isso or Facebook comments. Want social integration? Add Twitter or Facebook’s JavaScript widget to your website. Want real-time data updating live on your website? Add a squirt of Firebase. Want search? Add Swiftype. Want to add live chat support? Slaaks is there. 

The list goes on and on, as a whole ecosystem of purely browser-based add-ons to websites is emerging.

### THE CDN IS GOING MAINSTREAM

When Akamai launched the first content delivery network in 1999, only the largest web properties in the world could afford to deliver their web assets from CDN edge nodes distributed all over the world. It wasn’t that long ago that CDNs were used only by companies at the scale of CNN and Facebook, rather than mere mortals.

While Akamai still has enterprise-level pricing, today anyone can sign up for Amazon AWS and put CloudFront on top of their website. Also, companies like Fastly, MaxCDN and CloudFlare offer CDN services at prices that even a small business can afford.

A static website can be readily deployed directly to a CDN and served straight from local caches near end users. Fiddling with the configuration still takes some time, and cache invalidation can be tricky, but it’s doable and can be completely automated with services such as ours

### PERFORMANCE IS A MUST

The explosion of mobile devices has changed the face of the web in many ways. More and more visitors are coming to the web from a mobile device, sometimes on a 3G connection. Never has performance been as important as it is now.

We all know this data: 57% of online visitors will abandon a page if it takes longer than 3 seconds to load. People used to be willing to wait up to 10 seconds, but expectations are way higher today. And on mobile, where there’s no multi-tasking and little else to do, waiting for a website to load is so frustrating that more than 4% of people report that they’ve physically thrown their phone while using a slow mobile website!

No matter how much you optimize a dynamic website for performance or how many thousand of dollars you throw at it, it will never give you the same basic performance guarantee as a well-tuned static website hosted right on a CDN for a few bucks a month. With performance constantly growing in importance, it’s no wonder that developers are looking for ways to pre-generate their HTML, instead of letting the server spend time and resources on generating a page for every single HTTP request.

Static website generation also eliminates a lot of performance concerns during the development process.

If you’re building a dynamic database-driven website, the efficiency of the database queries you’re making is extremely important because they’ll need to be fast enough to run once for every single HTTP request. Even if a solid caching layer lies on top of your website, there’s often a risk that some requests will effectively work as cache-busters, triggering worst-case queries in the back end and causing the whole system to grind to a halt.

With a static-generated website, it doesn’t matter much if pulling content into a template takes a few seconds more or less: That only happens when you publish, and there will never be a performance penalty for end users.

### The Final piece of the Puzzle

The final piece of the puzzle, however, is content editing. While working directly in Markdown in a text editor and pushing to GitHub is close to the ideal workflow for a front-end developer, it’s not something you’d get normal, non-technical end user to participate in. 

Systems such as Contentful, Prismic.io and GatherContent decouple the CMS layer from the actual website builder. This makes them really interesting tools for multi-channel content management, where you’re writing content not just for a particular website, but also for a mobile app, a Facebook page or a white paper. Publishing new content triggers a webhook in a build system; then, a static website generator runs the build and fetches data from the content API; and the result is pushed straight to a CDN.

The ultimate answer is an open-source Static CMS system without any lock-in to a particular static website generator, Git host or hosting platform. It will be a great way to push the limit of what kind of website you can build with modern static website technology.