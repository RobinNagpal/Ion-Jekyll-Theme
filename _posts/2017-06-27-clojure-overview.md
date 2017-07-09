---
layout: post
title:  "Clojure Overview"
date:   2017-06-27 23:37:44
categories: clojure
---

## Overview

### Clojure Namespace
* Generally Clojure names space maps to Clojure files defines as (ns intro)

### Clojure Evaluation
* Normal Java Evaluation  `Source Code --> Converted to Byte code by compiler --> Byte Code is then run by JVM`
* Clojure Evaluation 
    * `Source Code --> Clojure Reader reads the code form File/REPL --> Reader converts to data structures`  
    * `Clojure Compiler takes it and converts  the data structures into the java byte code --> Byte Code is then run by JVM`

### Operation Forms
* `(op ...)` 
* Operation forms are used to call function in Clojure
* It consists List style left and right parentheses,  op (operation) in the first position and after that there can be zero or more arguments
* op can be one of three
    * Special Operator(operations built into Clojure) or macro (Operations that return Clojure code)
    * Expression that yields a function
    * Something invocable

### Structure vs Semantics
* Clojure treats code as data
* Structurally `(+ 3 4)` can be treated as `() as list`, `+ as symbol` and `3 4 as numbers`
* Semantically  `(+ 3 4)` can be treated as `() as invocation`, `+ as operation` and `3 4 as Arguments`

**In Clojure space is treated as comma**
`(+ 3 4) is same as (+, 3, 4) or (+,3,4) `

### Literals
* `42 is Long`
* `6.123123123 is Double`
* `42N is BigInt`
* `1.0M is BigDEcimal`
* `22/7 is Ratio`
* `"Hello" is String`
* `\e is Character`
* `true false is Boolean`
* `nil is null`
* `* Fred *bob* are Symbols (*bob* means bob is mutable)`
* `:alpha :beta are Keywords (used as keys for maps and dictionaries)`

### Data Structures
* `(4 :alpha 3.0) is a List`
* `(4, :alpha, 3.0) is also a List`
* `[2 "Hello" 99] is a Vector (Similar to Array)`
* `{:a 1,:b 2} is a Map`
* `{:a 1 :b 2} is also a Map`
* `#{alice jim bob} is a Set`

Clojure collections are heterogenously typed
 
## Metadata 
Clojure allows to add metada to any object. These maps of Metadata has no effect on objects equality

* `(with-meta [1 2 3] {:example true}) means {:example true} map is added to vector [1 2 3] `
* `(meta (with-meta [1 2 3] {:example true})) can be used to print metadata`

Metadata can be used to store things like function documentation strings

## Reader Macros 
Clojure knows how to expand reader macros to larger pieces of Clojure code
* `'foo represents (quote foo)`
* `#'foo represents (var foo)`
* `@foo represents (deref foo)`
* `#(+ % 5) represents (fn [x] (+ x 5))`
* `^{:key val} foo  represents (with-meta foo {:key val})`
* `^:key foo represents (with-meta foo {:key true})`



