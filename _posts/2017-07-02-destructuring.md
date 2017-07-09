---
layout: post
title:  "Clojure Destructuring"
date:   2017-07-02 23:37:44
categories: clojure
---

## Destructuring

Destructuring provides a way to pull apart compound data. Its a neat alternative to explicit and more verbose access of data.
Destructuring works for both sequential and associative data structures. Destructuring also works for deep/nested access. 
Destructuring binds to nil if there is no data.

### Sequential Destructuring
```
    (def a-vector [2 3 4 5 6 7])
    (let [[a b c] a-vector] (println a b c))        ;;=> 2 3 4
```

```
    (def a-vector [2 3])
    (let [[a b c] a-vector] (println a b c))        ;;=> 2 3 nil
```

### use `&` - Everything else
```
    (def a-vector [2 3 4 5 6 7 8])
    (let [[a & everyThing] a-vector] (println a everyThing))  ;;=> 2 (3 4 5 6 7 8)
```

### `_` to ignore
```
    (def a-vector [2 3 4 5 6 7 8])
    (let [[_ _ & everyThing] a-vector] (println everyThing))       ;;=> (4 5 6 7 8)
```

### Destructuring in function arguments
```
    (def a-vector [2 3 4 5 6 7 8])
    
    (defn printAfter3 [[_ _ & others]] (println others))
    (printAfter3 a-vector)      ;;=> (4 5 6 7 8)
```

### Associative destructuring
```
    (def a-map {:a 1 :b 2 :c 5})
    
    (defn printAfter3 [{c :c }] (println c))
    (printAfter3 a-map )        ;;=> 5
```

using `:keys`

```
    (def a-map {:a 1 :b 2 :c 5})
    
    (defn printAfter3 [{:keys [c]}] (println c))
    (printAfter3 a-map )
```

```
    (def a-map {:a 1 :b 2 :c 5})
    
    (defn printAfter3 [{:keys [c, d]} ] (println c d))
    (printAfter3 a-map )        ;;=> 5 nil
```

Providing defaults with `:or`
```
    (def a-map {:a 1 :b 2 :c 5})
   
   (defn printAfter3 [{:keys [c, d] :or {d 20}} ] (println c d))
   (printAfter3 a-map )         ;;=> 5 20
```

### Named Arguments
```
(defn addA&E [{:keys [a e]}] (+ a e) )
(println (addA&E {:a 1 :b 2 :c 3 :d 4 :e 5 :f 6}))      ;;=> 6

(defn addC&EInOther [a, b & {:keys [c e]}] (+ c e) )
(println (addC&EInOther :a 1 :b 2 :c 3 :d 4 :e 5 :f 6))     ;;=> 8
```

