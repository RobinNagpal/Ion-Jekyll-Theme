---
layout: post
title:  "Introduction to Senna.js"
date:   2015-08-28 14:37:44
categories: Web Development
---

### Problem Statement
As we have seen in the last blog that the architecture of SPA greatly differs from the architecture of conventional apps. Hence, SPA approach works fine with the application that needs to be developed from scratch. But refactoring of the huge application that have already been developed is sometimes not feasible. For project that had costed around $10 million, making it SPA can cost another $2 million. Now this is just the upfront cost. Then there will be opportunity cost as for the next 6 months or an year, there might be no new features  as most of the team would be involved in refactoring. 

Due to this huge investments, companies often don’t take this route. 
### Senna.js
As I have mentioned that its sometimes impractical to do the big rewrite to make your application as single page app. Senna.js provides a nice alternative to the SPA approach that most of us are familiar with. It heavily exploits HTML5 History API.

Senna.js is based on the concept of surfaces, i.e. you register the surfaces that needs to change, and whenever user does anything relevant, the browser sends an AJAX request to get the full page in the conventional way and then it replaces the old surfaces with the new HTML

### Let's see in detail how it works

* Step 1) When the page loads we mention the surface Ids, which is actually div id, and the URLS that need to be intercepted. 
* Step 2) When user does an action i.e. clicks a link, Senna.js intercepts the action and instead of sending a full page load request, it sends the request in the form of Ajax.
* Step 3) It shows UI feedback, informing the user that the content is loading
* Step 4) It reads the returned HTML from the server and parses the new HTML returned for the registered surfaces
* Step 5) It then flips or replaces the existing or old surfaces with the new ones that are returned 
* Step 6) It then updates the URL programmatically via Javascript and completes the rendering

We can represent the above flow as :
<img src="{{ site.baseurl }}/images/posts/2015/senna-js/senna.js.png" class="half-fit image">

So comparing it to the famous SPA frameworks we can see that there are very few changes required on the server side or client side. The changes that are required are related to including of Senna.js and registering of surfaces & URLs.

With just 150-200 lines of code, you can make your existing applications as SPA. This statement holds true for the existing enterprise level web applications also.

### Drawbacks:

There are couple of drawbacks to this approach.

1. The browser needs to support history API. Browser traffic wise there are nearly 8-10% of the users still use old browser which doesn’t support history API. For them the old app will continue to work in the same way i.e. with SPA benefits.
2. Difficult to have SPA behavior for the websites that does’t have common surfaces within  the pages.  
 