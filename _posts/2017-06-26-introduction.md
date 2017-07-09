---
layout: post
title:  "Introduction to Clojure"
date:   2017-06-26 23:37:44
categories: clojure
---


##Introduction to Clojure
I just started working and clojure and I am writing a series of blogs just for my self so that if I want to refer to someting quickly, I can have a look. 

There and some nice books and tutorials that can help you in learning about clojure. This blog series will give you a good head start on clojure.
 
### Average Function in Clojure
```
(defn average
[numbers]
(/ (apply + numbers) (count numbers)))
```

1. The particular usage of parentheses to delimit scope, rather than the more familiar braces {...} or do ... end blocks
2. The use of prefix notation indicating the operation being performed; e.g., (+ 1 2) rather than the familiar infix 1 + 2

### Expressions, Operators, Syntax, and Precedence
All Clojure code is made up of expressions, each of which evaluates to a single value. 
This is in contrast to many languages that rely upon valueless statements—such as if, for, 
and continue—to control program flow imperatively. Clojure’s corollaries to these
statements are all expressions that evaluate to a value.



1. Lists (denoted by parentheses) are calls, where the first value in the list is the operator
and the rest of the values are parameters.
2. Symbols (such as average or +) evaluate to the named value in the current scope—
which can be a function, a named local like numbers in our average function, a Java
class, a macro, or a special form. 
3. All other expressions evaluate to the literal values they describe.

### Compare Clojure with Java
Clojure expression
```
(not k)
(inc a)
(/ (+ x y) 2)
(instance? java.util.List al)
(if (not a) (inc b) (dec b))
(Math/pow 2 10)
(.someMethod some Obj "foo" (.otherMethod otherObj 0))
```

Java
```
!k
a++, ++a, a += 1, a + 1a
(x + y) / 2
al instanceof java.util.List
!a ? b + 1 : b - 1
Math.pow(2, 10)
someObj.someMethod("foo", otherObj.otherMethod(0))
```


