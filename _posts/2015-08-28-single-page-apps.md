---
layout: post
title:  "What are Single Page Apps ?"
date:   2015-08-28 11:37:44
categories: update
---
Single page apps or Websites are the websites that load the page upon first request and there is no page refresh on all the subsequent actions of the user. So when the first request goes to the server, the server responds with an HTML page which has link to one of the JavaScript Frameworks. 

This Javascript frameworks when loaded in the browser,  reads the URL/route and based on it shows the relevant view.  If user now clicks on any of the buttons or links, the Javascript frameworks normally intercepts them and then accordingly loads the uncompiled view partial and JSON. It then combines the uncompiled view partial with the data and then returns it to the user. 

This is very different form the conventional MVC frameworks whose architecture looks like this.
<img src="{{ site.baseurl }}/images/posts/2015/spa/Conventional_Architecture.png" class="half-fit image">

So rather than server deciding, what needs to be shown next, its the client JavaScript framework that decides that when should be shown next. The architecture of the SPA apps looks like this
<img src="{{ site.baseurl }}/images/posts/2015/spa/SPA_Architecture.png" class="half-fit image">
