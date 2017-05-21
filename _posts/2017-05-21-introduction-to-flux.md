---
layout: post
title:  "Introduction to Flux"
date:   2017-05-21 14:37:44
categories: javascript
---

### Background
So far one of the most common architectural patterns that have been used in the we has been MVC. 
Though MVC has been used for last couple of decades, with the new highly interactive websites/apps it doesn't scale that well. 
With the increasing number of model and views the relation between them no longer remains one to one and it sort of becomes like a web.
<img src="{{ site.baseurl }}/images/posts/2017/introduction-to-flux/mvc-problems.jpeg" class="half-fit image">



### Introduction to flux
Flux simplifies it by providing more of a single directional data flow. This avoids a lot of the arrows that go into both directions.

<img src="{{ site.baseurl }}/images/posts/2017/introduction-to-flux/flux-simple-diagram.png" class="half-fit image">

What we have here is 
1. **Action**  action corresponds to some action occurring on the UI. 
2. **Dispatcher** is sort of the central traffic controller to the application
3. **Store** which maintains the data for the application 
4. **View** the view which is shown to the user and that re-render whenever the data changes in the store
 
When ever anything now happens on the View then then create a new action and give it to the dispatcher.
Dispatcher makes sure that there are no cascading effects, which means that dispatcher accepts the next action after it has finished processing the store for the current action. And this  is the biggest difference between MVC and Flux.

The simplicity we get by using Flux is because flow is just in one direction.

A more general view of Flux looks like this

<img src="{{ site.baseurl }}/images/posts/2017/introduction-to-flux/flux-general-view.png" class="half-fit image">

In MVC model its very difficult to have a simplified view like above for a complex application

In flux, now the logic for updating of the data lives closer to the data store

### Key code snippets of a Flux app

##### Registering your component with Store
```javascript 1.6
  componentDidMount: function(){
    todoStore.addChangeListener(this._onChange);
  }
  
  _onChange: function(){
      this.setState({
        list: todoStore.getList()
      })
  }
```

##### Actions

```javascript 1.6
    var AppDispatcher = require('../dispatcher/AppDispatcher');
    var todoActions = {
      addItem: function(item){
        AppDispatcher.handleAction({
          actionType: appConstants.ADD_ITEM,
          data: item
        });
      }
    }
```

##### Constant

```javascript 1.6
    var appConstants = {
      ADD_ITEM: "ADD_ITEM",
      REMOVE_ITEM: "REMOVE_ITEM"
    };
```

##### Dispatcher

```javascript 1.6
    var Dispatcher = require('flux').Dispatcher;
    var AppDispatcher = new Dispatcher();
    
    AppDispatcher.handleAction = function(action){
      this.dispatch({
        source: 'VIEW_ACTION',
        action: action
      });
    };
```

##### Store - store has four parts

1. The actual “model” or data store

```javascript 1.6
    var _store = {
      list: []
    };
```

2. Setter methods

```javascript 1.6
    var addItem = function(item){
      _store.list.push(item);
    };
    
    var removeItem = function(index){
      _store.list.splice(index, 1);
    }
```
3. The Store itself

```javascript 1.6
    var todoStore = objectAssign({}, EventEmitter.prototype, {
      addChangeListener: function(cb){
        this.on(CHANGE_EVENT, cb);
      },
      removeChangeListener: function(cb){
        this.removeListener(CHANGE_EVENT, cb);
      },
      getList: function(){
        return _store.list;
      },
    });
```

4. Action handlers

```javascript 1.6
    AppDispatcher.register(function(payload){
      var action = payload.action;
      switch(action.actionType){
        case appConstants.ADD_ITEM:
          addItem(action.data);
          todoStore.emit(CHANGE_EVENT);
          break;
        case appConstants.REMOVE_ITEM:
          removeItem(action.data);
          todoStore.emit(CHANGE_EVENT);
          break;
        default:
          return true;
      }
    });
```