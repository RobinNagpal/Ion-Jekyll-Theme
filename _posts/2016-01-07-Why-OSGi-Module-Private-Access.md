---
layout: post
title:  "Why OSGi - Part 1 : Module - Private Access"
date:   2016-01-07 14:37:44
categories: Java
---

The access modifiers for Java are of real help for smaller projects, But for enterprise level projects they don’t suffice the needs. Let’s try to understand by taking some examples. Suppose you are working on a multi module project is which you create JARs for each module, and then use these JARs in a parent project. Each of these JARs will consist of several packages.

Ideally, for the classes that you write in these JARs, you would want to have two type of modifiers

1. Public (Module-Private)  - Modifier that allows classes to be used across the packages, but just within the module.
2. Public-Public (Module-Public) - Modifier that allows classed to be used across the packages within and outside the module. This access modifier could only be provided to API classes, i.e. classes which we know will be used outside the module. While coming up with future releases, you will have to make sure that these classes are backward compatible as it would be used by other modules.


Unfortunately, amongst the two, Java just has a PUBLIC access modifier which provides global access(Public-Public), i.e. across the packages and across the modules.  This could seem fine for smaller projects, but when you are working on projects where your code will be used by multiple clients or teams, this could lead to a lot of side effects. The most common is that other teams will be using the classes which were PUBLIC, but were intended to be used just within the module. Now you will have to make sure that these classes will also be backward compatible. If you are developing your enterprise software the normal Java way you will have this type of design.

<img src="{{ site.baseurl }}/images/posts/2016/why-osgi/before.png" class="half-fit image">

The above diagram can help us understand the problem if we are just using plain Java. Other modules can use any of the public classes and functions of your JARs, even though your intention was that only some of those classes and functions to be exposed outside the Module/JAR.  This problem seriously impacts the flexibility and the development speed.



OSGI rescues us from this problem. Within every OSGI module, you have to explicitly declare the packages your module needs to import and the packages your module can export. So neither can anyone use your public classed, not can you use any of the public classes of other module unless explicitly mentioned. Following lines in MANIFEST.MF of OSGI modules dictate the exporting and importing of the packages.


```
Import-Package: org.osgi.framework;version="1.3.0"

Export-Package: com.echofex.osgi.model, com.echofex.osgi.service
```

After using OSGI for each of the modules, this is how you modules will look like.

<img src="{{ site.baseurl }}/images/posts/2016/why-osgi/after.png" class="half-fit image">

You can now see that the internals of the modules are completely hidden from other modules. Also, you don’t have to think of these modules as just JAR files. In normal scenarios, modules are a bit bigger, constituting a separate functionality and each might consist of multiple JARs.