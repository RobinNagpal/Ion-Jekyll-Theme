---
layout: post
title:  "Clojure Functions"
date:   2017-06-28 23:37:44
categories: clojure
---

## Functions

In Clojure functions are treated as first class citizens i.e. function is treated like any other value and can be passed over.
This allows building higher order functions.

Its common in Clojure to have pure functions, i.e. functions with no side effects

### Anonymous functions
`fn` creates an anonymous function with named parameters and body e.g.
* `(fn [message] (print message))` declares a function without name, one argument `message` and `print message` as body

There can be zero or more arguments in the arguments vector and there can be one or more expressions in the body

We cant refer to the anonymous function in other parts of the code. But we can invoke a `fn`(anonymous function)
in function position e.g. `((fn [message] (print message)) "Hello World!")`


### Defining Named functions using `defn`
```
 ;; Define a messenger function
 (def messenger (fun [msg] (print msg)))


 
 ;; Other way to do the same
 (defn messenger [msg] (print msg))
 
 ;; calling the function
 (messenger "Hello World!")   
```

`defn` is a short hand for saying I'am defining a function


### let
* `let` binds symbol to immutable values. Values can be literals or expressions
* Bound symbols are availabel in the lexical scope

```
(defn messenger [msg]
    ( let [ a 7
            b 5
            c (capitalize msg)]
                   
       (println a b c)

    ) ; end of let scope
) ; end of function

```

### Arity 
Arity means the number of arguments a function takes

* Functions can be overloaded by arity
* Each arity is a `list:([args*] body*)`

```
 (defn messenger 
 
 ;; no args function which calls one arg function
 ([] (messenger "Hello Wrold !"))
 
 ;; one arg function
 ([msg] (println msg)))
 
 (messenger) ;; "Hello world"
 
 (messenger "Hello Class") ;; "Hello Class"

```

### Variadic functions - functions with variable number of arguments
* Variadic function is of indefinite arity
* Only one allowed when overloading on arity
* `&` symbol in params
* Next param collects all remaining args
* Collected args are represented as sequence

```
 (defn messenger [greeting & who] 
    (print greeting who))
    
 (messenger "Hello" "World" "Class")
```

### Apply
* Invokes function on arguments
* Final argument is a sequence
* "Unpacks" remaining arguments from sequence

```
(let [f print
      a 1
      b 2
      more '(3 4)]
  (apply f a b more))
  
```

```
  (defn messenger [greeting & who] (apply print greeting who))
  
  (messenger "Hello" "World" "Class")
  ;; Hello World Class  
```

### Closure
```
(defn messenger-builder [greeting]
  (fn [who] (print greeting who)))

(def helloer (messenger-builder "Hello"))

(helloer "World!")
```

```
(defn messenger-builder [greeting]
  (fn [who] (print greeting who)))

(defn helloer [] (messenger-builder "Hello"))

((helloer) "World!")
```

Both are same versions of the code. One uses `def` and other users `defn`


### Invoking Java Code
* Instantiation `(Widget. "foo")` is same as `new Widget("foo")`
* Instance method `(.nextInt rnd)` is same as` `rnd.nextInt()` 
* Instance field `(.-field object)` is same as `object.field`
* Static method `(Math/sqrt 25)` is same as `Math.sqrt(25)`
* Static field `Math/PI` is same as `Math.PI`

### Method Chaining
`(.. person getAddress getZipCode)` is same as `(.getZipcode (.getAddress person))` is same as java version : `person.getAddress().getZipCode()`  

### Terse form `#()` for short functions
`#(.length %)` is same as (fn [obj] (.length obj))`