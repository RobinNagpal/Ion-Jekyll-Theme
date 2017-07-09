---
layout: post
title:  "Clojure Collections"
date:   2017-07-01 23:37:44
categories: clojure
---


## Collections

Clojure has support for lists, maps, sets and vectors. Clojure collections are immutable.
Instead of mutating the collection, Clojure function takes arguments and returns a new collection without affecting the original.
Any of these collections can be represented with Seq abstraction

### Persistent Data Structures
* New values are built from old values + modifications
* New values are not full copies
* New values and old value are both available after changes
* All Clojure collections are persistent

### Sequential and Associative data structures
* **Sequential**  - List, Vector
* **Associative** - Map, Vector
Both support declarative destructuring

### List
```
()                  ;=> empty list
(1 2 3)             ;= error because 1 is not a function
(list 1 2 3)        ;=> (1 2 3)
'(1 2 3)            ;=> (1 2 3)
(conj '(2 3) 1)     ;=> (1 2 3)  conj adds element to collection in most efficient way. For list its adds at front
```

### Vector
```
[]                  ;=> empty vector
[1 2 3]             ;=  [1 2 3]
(vector 1 2 3)      ;=> [1 2 3]
(vec '(1 2 3))      ;=> [1 2 3]  vec converts list to vector
(nth [1 2 3] 1]     ;=> 2
(conj '[2 3] 1)     ;=> [2 3 1]  For vector conj adds at the end 
```

### Map
```
{}                      ;=> empty map
{ :a 1 :b 2}            ;=> { :a 1 :b 2} 
(:a { :a 1 :b 2})       ;=> 1
({ :a 1 :b 2} :a)       ;=> 1
(assoc { :a 1} :b 2)    ;=> { :a 1 :b 2}
(dissoc { :a 1} :a)     ;=> {}
(conj {} [:a 1])        ;=> {:a 1}
```

```
(def jdoe {:name "John Doe" :address {:zip 33455}})
(get-in jdoe [:address :zip])
(assoc-in jdoe [:address :zip] 27514)
(update-in jdoe [:address :zip] inc)
```

### Set
```
#{}                     ;=> empty set
#{:a :b}                ;=> #{:a :b}
(#:{:a :b} :a)          ;=> :a 
(conj #{} :a)           ;=> #{: a}
(contains? #{:a} :a)    ;=> true
```


### Concise Collection Access
Since Clojure collections are functions there are many concise ways to work on collections

`(get [:a :b :c] 2)`  is equivalent to `([:a :b :c] 2)`
`(get {:a 5 :b 6} :c 7)` is equivalent to `([({:a 5 :b 6} :c 7)`

Collection keys are (often) functions

`(get {:a 5 :b 6} :b)` is equivalent to `(:b {:a 5 :b 6})`
`(get {:a 5 :b 6} :c 7)` is equivalent to `(:c {:a 5 :b 6} 7)`
