---
layout: post
title:  "if, kenapa spesial?"
date:   2024-03-17 11:10:00 +0700
---
`if`, kenapa spesial? coba baca `doc` yang disediakan di `REPL`, boleh dicek juga [link-nya](http://clojure.org/special_forms#if):
```clojure
user> (doc if)
-------------------------
if
  (if test then else?)
Special Form
  Evaluates test. If not the singular values nil or false,
  evaluates and yields then, otherwise, evaluates and yields else. If
  else is not supplied it defaults to nil.

  Please see http://clojure.org/special_forms#if
nil
```
Kalo tidak spesial--`if` akan dievaluasi seperti `function` pada umumnya--semua argumen yang diinput akan menjadi argumen untuk function, dalam hal ini `if` dengan 3 argumen: `test, then, else?`--dan ini benar kalo kita melihat bagaimana struktur ekspresi yang kita input:
```clojure
user> (if true 1 2)
1
```
Bandingin dengan:
```clojure
user> (+ 1 2 3 4 5 6 7 8 9)
45
```
`if` menerima `test` sebagai argumen, kemudian berdasarkan `test`, akan memilih ekspresi `then` atau `else?`, itu makanya dia spesial--dia ngga bisa disamain sama function `+` misalnya--bahkan ekspresi `else?` itu bukan mandatori--dengan default `nil`--lihat `tanda tanya (?)` itu, jurang antara aku (ah!, Rangga--AADC).

Gimana dengan `when`? `when` adalah `if` tanpa ekspresi `else?`.
```clojure
user> (defmacro when
        [condition & body]
        `(if ~condition (do ~@body)))
#'user/when
user> (when true "I love you!")
"I love you!"
user> (when false "I love you!")
nil
user> (macroexpand '(when true "I love you!"))
(if true (do "I love you!"))
user> (macroexpand '(when false "I love you!"))
(if false (do "I love you!"))
```
Gimana dengan `unless`?
