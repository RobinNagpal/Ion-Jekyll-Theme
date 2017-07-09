---
layout: post
title:  "Clojure Destructuring"
date:   2017-07-03 23:37:44
categories: clojure
---

## Sequences
Clojure provides sequence abstraction over many of its data structures(even maps) which provides a lot of functions
and helps working with sequential things

* Sequences are abstraction for representing iterations
* Sequences can be backed by data structures or functions
* When backed by functions, they can be lazy and infinite
* Its a foundation for large library functions

### Sequence API
* `(seq col)` take collection and return next
* `(first coll)` return first element
* `(rest coll)` take out first and return rest
* `(cons x coll)` returns a new collection with x as first element e.g. `(println (cons "a"  ["l", "s", "e"]))      ;;=>(a l s e)`

### Sequence Functions
Sequence functions can be divided roughly into two categories.
1. Generators - generators are used to generate lazy sequences from the data, functions, or other objects provided
e.g. list, vector, map, SQL ResultSet, Stream, Directory etc.  
2. Operations - operations and functions that perform some operation and return another sequence or some other data structure e.g
map, reduce, filter, count, some, replace



### for
