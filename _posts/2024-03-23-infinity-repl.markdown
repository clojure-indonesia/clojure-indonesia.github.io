---
layout: post
title:  "Infinity (REPL)"
date:   2024-03-23 18:13:00 +0700
---
```clojure
user> (doc range)
-------------------------
clojure.core/range
([] [end] [start end] [start end step])
  Returns a lazy seq of nums from start (inclusive) to end
  (exclusive), by step, where start defaults to 0, step to 1, and end to
  infinity. When step is equal to 0, returns an infinite sequence of
  start. When start is equal to end, returns empty list.
nil
```
`range`--function dengan `multi-arity`--bisa diinvoke tanpa parameter, dengan parameter `end`, dengan `start` dan `end`, dengan `start` dan `end` diikuti `step`.
```clojure
user> (range 10)
(0 1 2 3 4 5 6 7 8 9)
```
```clojure
user> (range 10 20)
(10 11 12 13 14 15 16 17 18 19)
```
```clojure
user> (range 10 20)
(10 11 12 13 14 15 16 17 18 19)
```
```clojure
user> (range 10 20 2)
(10 12 14 16 18)
```
Gimana kalau `range` diinvoke tanpa parameter?
```clojure
user> (range)
```
Infinity!, biasanya cara nge-kill infinity di REPL dengan di-force close, kemudian buka REPL lagi. Sebenarnya ada cara yang simpel dan cakep--dengan mengatur panjang print (_*print-length*_) secara manual:
```clojure
user> (set! *print-length* 20)
20
```
```clojure
user> (range)
(0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 ...)
```
```clojure
user> (cycle (range 3))
(0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 ...)
```
```clojure
user> (iterate #(+ % 3) 30)
(30 33 36 39 42 45 48 51 54 57 60 63 66 69 72 75 78 81 84 87 ...)
```
_See!_  
PS: syntax-highlight-nya ngeselin--`0 10 10 10 0 0 30` diwarnai sebagai function!
