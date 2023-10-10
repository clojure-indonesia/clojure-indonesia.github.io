---
layout: post
title:  "Halo, Dunia!"
date:   2023-10-10 14:02:00 +0700
---

```clojure
"Halo, Dunia!"
```
```clojure
(defn halo
  []
  "Hallo, Dunia!")

(halo)
```
```clojure
(def halo-dunia-pake-lambda
  (fn []
    "Halo, Dunia!"))

(halo-dunia-pake-lambda)
```
```clojure
(#(apply str %&) "Halo, " "Dunia!")
```