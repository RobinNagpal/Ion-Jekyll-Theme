---
layout: post
title:  "Redux vs Flux"
date:   2017-05-21 21:37:44
categories: javascript
---

### Flux
Flux simplifies the application by providing more of a single directional data flow. This avoids a lot of the arrows that go into both directions.

<img src="{{ site.baseurl }}/images/posts/2017/redux-vs-flux/flux-simple-diagram.png" class="half-fit image">

What we have here is 
1. **Action**  action corresponds to some action occurring on the UI. 
2. **Dispatcher** is sort of the central traffic controller to the application
3. **Store** which maintains the data for the application 
4. **View** the view which is shown to the user and that re-render whenever the data changes in the store
 
When ever anything now happens on the View then then create a new action and give it to the dispatcher.
Dispatcher makes sure that there are no cascading effects, which means that dispatcher accepts the next action after it has finished processing the store for the current action. And this  is the biggest difference between MVC and Flux.

The simplicity we get by using Flux is because flow is just in one direction.

### Redux


### Redux vs Flux


| Flux                                   | Redux                              | 
|:-------------------------------------- |:---------------------------------- |
| Store contains state and change logic  | Store and change logic are separate| 
| Multiple Stores                        | Single Store                       |
| Flat disconnected Stores               | Single store with hierarchical reducers|
| Singleton Dispatcher                   | No dispatcher                      |
| State is mutated                       | State is immutable                 |
| React components subscribe to stores   | Container components utilize connect|

**Benefits of Redux over Flux**
1. Flux makes it unnatural to reuse functionality across stores
2. In Flux, stores are flat, but in Redux, reducers can be nested via functional composition
3. Hot reloading is very difficult in Flux. When Redux needs to reload the reducer code, it calls replaceReducer(), and the app runs with the new code. 

**Benefits of Flux over Redux**
1. Much easier to understand and get started