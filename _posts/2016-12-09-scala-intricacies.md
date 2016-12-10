---
layout: post
title:  "Scala Intricacies"
date:   2016-12-09 12:37:44
categories: scala
---

##### Unit
Scala compiler can convert any type to Unit. For example, if the last result of a method is a String, but the method’s result type is declared to be Unit, the String will be converted to Unit and its value lost.

##### Singleton Objects
Each singleton object is implemented as an instance of a synthetic class referenced from a static variable, so they have the same initialization semantics as Java statics.
In particular, a singleton object is initialized the first time some code accesses it.

##### Companion Objects
When singleton object has the same name as class and is defined in the same source, its call ed as companion object. 
A class and its companion object can access each other’s private members. 

