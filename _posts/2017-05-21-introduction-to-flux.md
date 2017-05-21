---
layout: post
title:  "Introduction to Flux"
date:   2017-05-21 14:37:44
categories: javascript
---

#### Background
So far one of the most common architectural patterns that have been used in the we has been MVC. 
Though MVC has been used for last couple of decades, with the new highly interactive websites/apps it doesn't scale that well. 
With the increasing number of model and views the relation between them no longer remains one to one and it sort of becomes like a web.
<img src="{{ site.baseurl }}/images/posts/2017/introduction-to-flux/mvc-problems.jpeg" class="half-fit image">
`ref - https://brigade.engineering/what-is-the-flux-application-architecture-b57ebca85b9e`


#### Introduction to flux
Flux simplifies it by providing more of a single directional data flow. This avoids a lot of the arrows that go into both directions.

What we have here is 
1. **Action**  action corresponds to some action occurring on the UI. 
2. **Dispatcher** is sort of the central traffic controller to the application
3. **Store** which maintains the data for the application 
4. **View** the view which is shown to the user and that re-render whenever the data changes in the store
 
When ever anything now happens on the View then then create a new action and give it to the dispatcher.
Dispatcher makes sure that there are no cascading effects, which means that dispatcher accepts the next action after it has finished processing the store for the current action. And this  is the biggest difference between MVC and Flux.

The simplicity we get by using Flux is because flow is just in one direction.

