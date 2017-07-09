---
layout: post
title:  "Clojure Namespaces"
date:   2017-06-29 23:37:44
categories: clojure
---


## Namespaces

Namespaces help us modularize the code in Clojure.
They help us divide things like functions or pieces of data into namespaces.
We use namespaces to define public and private functions/members

Namespaces allow us to declare Vars, keywords and Java type names in a particular scope,
which is not possible by using function arguments or `let`


### Vars
Vars are things that are created when we use `def` or `defn` inside the namespace.
Vars is an object that represent a named value and are stored in the namespace.


### Keywords
Keywords are lightweight strings that evaluate themselves. Keywords can also be namespace qualified
```
 ;; In the namespace "foo.bar"
 :x        ; Keyword with no namespace
 ::x       ; Keyword with "foo.bar" namespace
 :baz/x    ; Keyword with "baz" namespace
```

### REPL namespace
REPL always starts in `user` namespace. We can use `in-ns` to switch to a namespace.
`in-ns` will create a namespace if it doesn't exist. 

### Namespace Operations
* Load - `require` find source in classpath and evaluates it
    ```
        ;; plain require to load another namespace
        (require 'clojure.string)
        (println (clojure.string/upper-case "Rob"))
        ;; ROB        
    ```
* Alias - can be used for have shorter aliases
    ```
        ;; use :as to create an alias
        (require '[clojure.set :as set-alias])
        (println (set-alias/union #{1 2 3} #{2 3 4 7}))
        ;; #{7 1 4 3 2}
        
        (require '[clojure.java.io :as io]
                 '[clojure.string :as stringy])
        (println (stringy/index-of "Rob" "b"))
        (println (io/file "file-name"))
        ;; #object[java.io.File 0x66f57048 file-name]    
    ```
* Refer - `use` copy symbol binding from another namespace into current namespace
    ```
        (use `clojure.string)
        (reverse hello)        
    ```
    ```
        (use `[clojure.string :only (join)])
        (join "," ["1", "2", "3"])        
    ```
* Import - make Java class available in current namespace so that they can be used without package prefix
    ```
        (import (java.io FileReader File))
        
        (FileReader. (File. "readme.md"))
    ```

### `ns`
`(ns Intro)` creates namespace and then do REQUIREs and IMPORTs. It refers all of `clojure.core` and imports all of `java.lang`
Clojure converts `Dots` in namespace to `/` and `Hyphens` to `underscores`

Use `require` with `ns`
```
    ;; use require with ns
    (ns my.clojure.project
        (:require [clojure.string :as stringy]))
        

    (println (stringy/upper-case "rob"))    
```
 
 Use `use` with `ns`
```
    (ns my.clojure.project
      (:use [clojure.string :only (upper-case)]))
    
    (println (upper-case "rob"))
```

Use `import` with `ns`
```
    (ns my.clojure.project
      (:import (java.io File)))
    
    (println (File. "new-file"))
```

### Private Vars
Private Vars can be declared by adding `^:private` metadata to a definition. `defn-` is a shortcut for `defn ^:private`.
Private prevents accidental refer with use

### `the-ns`
To get access to namespace we use `the-ns`
  
```
    (the-ns `my.clojure.project)
```
 
 