---
layout: post
title:  "Clojure Abstractions"
date:   2017-06-30 23:37:44
categories: clojure
---

## Collection Abstractions

### Different type of abstractions for clojure collections
* Collection
* Sequence
* Associative
* Indexed
* Stack
* Set
* Sorted


### Collection
* `conj` to add an item to a collection
* `seq` to get a sequence of a collection
* `count` to get the number of items in a collection
* `empty` to obtain an empty instance of the same type as a provided collection
* `=` to determine value equality of a collection compared to one or more other collections

### Sequence
* `seq` produces a sequence over its argument.
* `first`, `rest`, and `next` provide ways to consume sequences.
* `lazy-seq` produces a lazy sequence that is the result of evaluating an expression.


We can get a sequence from 
* All Clojure collection types
* All Java collections (i.e., java.util.*)
* All Java maps
* All java.lang.CharSequences, including Strings
* Any type that implements java.lang.Iterable7
* Arrays
* nil (i.e., null as returned from Java methods)
* Anything that implements Clojure’s clojure.lang.Seqable interface

### Associative
The associative abstraction is shared by data structures that link keys and values in
some way. 

Maps and vectors are both associative collections, where vectors associate values with indices

* `assoc`, which establishes new associations between keys and values within the given collection - `(assoc map :new-key 4)`
* `dissoc`, which drops associations for given keys from the collection - `(dissoc map :new-key 4)`
* `get`, which looks up the value for a particular key in a collection - `(get map :a-key)`
* `contains?`, which is a predicate that returns true only if the collection has a value associated with the given key - `(contains? {:a 5 :b 6} :b)`

### Indexed
Indexed abstraction consists of a single function, nth, which is a specialization of `get`. 
They differ on how they deal with out-of-bounds indices: nth throws an exception while get returns nil


### Stack
Stacks are collections that classically support last-in, first-out (LIFO) semantics.
Clojure doesn’t have a distinct stack data structure, but it does support a stack abstraction via three operations:
* `conj`, for pushing a value onto the stack (conveniently reusing the collection-generalized operation)
* `pop`, for obtaining the stack with its top value removed
* `peek`, for obtaining the value on the top of the stack

### Set
Sets are treated as a sort of degenerate map, associating keys with themselves
```
(get #{1 2 3} 2)
;= 2
```
Set abstraction requires disj, which removes value(s) from the given set:
```
(disj #{1 2 3} 3 1)
;= #{2}
```

### Sorted
Only maps and sets are available in sorted variants. They do not have any literal notation;
they may be created by `sorted-map` and `sorted-set`, or `sorted-map-by` and `sortedset-by` 
if you provide your own predicate or comparator to define sort order.

* `rseq`, which returns a seq of a collection’s values in reverse, with the guarantee that doing so will return in constant time
* `subseq`, which returns a seq of a collection’s values that fall within a specified range of keys
* `rsubseq`, the same as subseq, but the seq is in reversed order
