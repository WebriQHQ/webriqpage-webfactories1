---
title: Post CMS Landscape
shortdesc: "Over the years, we've tried everything from Wordpress, Drupal, Squarespace, custom development app and we came all the way back to a Static approach. There's been quite a groundswell of belief over the past couple of years, we've been doing it all wrong. We've been making servers do all sorts of stuff they shouldn't be doing."
cmsUserSlug: ""
date: 2016-03-24T16:00:00.000Z
banner: /img/uploads/landing-page2.jpg
categories: recent-blog
writer: Philippe Bodart
---

### The Challenge 

<p>Over the years, we've tried everything from Wordpress, Drupal, Squarespace, custom development app and we came all the way back to a Static approach.</p>

There's been quite a groundswell of belief over the past couple of years, we've been doing it all wrong. We've been making servers do all sorts of stuff they shouldn't be doing.

The move to static worked out very well from a development perspective. It simplifies the development work, lowers the hosting costs, and ensures a high level of performance, scalability, and reliability.

In order to make this idea work at a large and on bigger projects, we needed to figure out how to automate the management, build, and deployment of static sites.

And we needed to pull this all together in manageable online tools. 

### Putting The Pieces Together

<p>We decided to use our own <a href="http://webriq.com" target="_blank">website</a> as a testing ground for using these tools. We migrated our content in to a repository on Github. In ordeback into our Roots project, we used an extension: <a href="https://github.com/carrot/roots-contentful" target="_blank">roots-contentful</a>. Every time our website was compiled, roots-contentful would fetch data through Contentful's API and pass it into our view templates. It would also compile each individual blog post's HTML file using the <a href="https://github.com/carrot/roots-contentful#single-entry-views" target="_blank">single page views</a> feature.</p>

With the Roots project now built on top of data from Contentful, we then set about automating deployment when content changed. First, we created a webhook endpoint that would start a new build and deploy the project whenever it received a POST request. Then, we set up a webhook in Contentful with the new Netlify endpoint as the destination URL. With this in place, every time an editor creates, deletes, or edits a new piece of content, we receive a webhook from Contentful and kicks off a new deploy. We run Roots compile, loads the new Contentful data with roots-contentful, optimizes our assets, and finally pushes it out to a global CDN. Within a couple minutes from publishing, our new content is live on our static site. Pretty cool.

The next step in our process is to provide content managers and publishers with an online User Interface to update the content directly in to the Github repository. Each time the content is updated and committed to Github, a new build will be started and the new or updated content will be published on the Static site. 

Whilst designing a website is the work of a designer, and coding it work for a developer, with the above approach we give content managers and content managers the needed tools to update the content via a simple browser based User Interface. The User Interface contains only the content elements that you want to manage, nothing more and nothing less. So, if you only need to change your blog, the UI will only contain the elements to manage your blog. If you have a more complex data model, it can contain all content elements of your website that you want to manage. The beauty is that you are not touching any of the codes of your website, only the relevant content elements. 

Beyond security, reliability and scalability, the other big advantage of the Static approach is versioning of your website. Since your entire site, from configuration to content, is file- based, it is very easy to keep all aspects of it within a version control system like Git. This can be especially advantageous for things like documentation that you may want to allow community contributions, for example, using pull requests on GitHub repository.

<p>You can see all the above in action on <strong><a href="http://app.webriq.com/auth/register" target="_blank">WebriQ APP</a></strong> or you can send us a <strong><a href="http://www.webriq.com/partners" target="_blank">DEMO REQUEST</a></strong></p>