---
layout: post
title:  "Scala - Classes and Objects"
date:   2016-12-09 12:37:44
categories: scala
---

##### Classes
```
class Employee {
    var name = "Name"
}

val employee = new Employee
```

##### Instance Variables
Fields are known as instance variables. 
Every instance gets its own set of variables. 
You can use ```val``` or ```var``` to define instance variables
By default instance variables are ```public```. Private fields can be declared as ``` private var name```


##### Method Parameters
Method parameters in scala are ```vals``` and not ```vars```. IF you attempt to reassign, it will not compile
The return statement at the end of the method is optional and can be dropped. Scala method returns the last value computed by the method
You can leave off the curly braces if a method computes only a single result expression. E.g. ```def getMonthlySalary = yearlySalary / 12```
If you leave off the equals sign before the body of a function, its result type will definitely be Unit
 
 
##### Singleton objects
Scala singleton looks like classes. But instead of ```class``` keyword it has ```object```
When singleton object has the same name as class and is defined in the same source, its call ed as companion object. 
A class and its companion object can access each other’s private members.
Singleton objects are like Java Classes with static methods. You use Singleton object name, a dot, and then the name of the method. 
Singleton object can extend calsses and mix in traits
One difference in a class and a singleton is that, Singleton cannot have parameters, primary because they cannot be instanciated 
