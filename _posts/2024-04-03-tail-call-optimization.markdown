---
layout: post
title:  "Tail-call optimization"
date:   2024-04-03 04:56:00 +0700
---
Before we start, eak aku taunya itu doang bahasa inggris, pastikan udah baca [recursion](https://clojure-indonesia.github.io/2024/04/01/recursion.html), dan ngalamin error ketika nyobain factorial dengan angka yang besar: `(factorial 100)` atau `(factorial 1000)` atau `(factorial 10000)` mungkin. Jangan lama-lama, kodenya mana dong?
```common-lisp
CL-USER> (defun factorial (n)
           (labels ((aux (n acc)
		              (if (zerop n)
			              acc
			              (aux (- n 1) (* acc n)))))
             (aux n 1)))
FACTORIAL
CL-USER> (trace factorial)
(FACTORIAL)
CL-USER> (factorial 10)
  0: (FACTORIAL 10)
  0: FACTORIAL returned 3628800
3628800
```
Bedanya apa dengan [recursion](https://clojure-indonesia.github.io/2024/04/01/recursion.html)?, emang gimana sih cara kerja recursion? cara kerja function? sangat penting untuk ngerti recursion terlebih dahulu, baru kemudian mulai mempelajari tail-call.

Sebagai pembanding, coba kita lihat lagi sebelum tail-call:
```common-lisp
CL-USER> (defun factorial (n)
	       (if (zerop n)
	           1
	           (* n (factorial (- n 1)))))
FACTORIAL
CL-USER> (trace factorial)
(FACTORIAL)
CL-USER> (factorial 10)
  0: (FACTORIAL 10)
    1: (FACTORIAL 9)
      2: (FACTORIAL 8)
        3: (FACTORIAL 7)
          4: (FACTORIAL 6)
            5: (FACTORIAL 5)
              6: (FACTORIAL 4)
                7: (FACTORIAL 3)
                  8: (FACTORIAL 2)
                    9: (FACTORIAL 1)
                      10: (FACTORIAL 0)
                      10: FACTORIAL returned 1
                    9: FACTORIAL returned 1
                  8: FACTORIAL returned 2
                7: FACTORIAL returned 6
              6: FACTORIAL returned 24
            5: FACTORIAL returned 120
          4: FACTORIAL returned 720
        3: FACTORIAL returned 5040
      2: FACTORIAL returned 40320
    1: FACTORIAL returned 362880
  0: FACTORIAL returned 3628800
3628800
```
Itu kan di Common LISP, gimana kalo di Clojure? kita bikin:
```bash
clojure -Sdeps '{:deps {org.clojure/tools.trace {:mvn/version "0.8.0"}}}'
```
```clj
user> (deftrace factorial
        [n]
        (loop [n n
               acc 1]
          (if (zero? n)
            acc
            (recur (dec n) (* acc n)))))
#'user/factorial
user> (factorial 10)
TRACE t412: (factorial 10)
TRACE t412: => 3628800
3628800
```
Sebelum tail-call, sebagai pembanding:
```clj
user> (require '[clojure.tools.trace :refer [deftrace]])
nil
user> (deftrace factorial
        [n]
        (if (zero? n)
          1
          (* n (factorial (dec n)))))
#'user/factorial
user> (factorial 10)
TRACE t422: (factorial 10)
TRACE t423: | (factorial 9)
TRACE t424: | | (factorial 8)
TRACE t425: | | | (factorial 7)
TRACE t426: | | | | (factorial 6)
TRACE t427: | | | | | (factorial 5)
TRACE t428: | | | | | | (factorial 4)
TRACE t429: | | | | | | | (factorial 3)
TRACE t430: | | | | | | | | (factorial 2)
TRACE t431: | | | | | | | | | (factorial 1)
TRACE t432: | | | | | | | | | | (factorial 0)
TRACE t432: | | | | | | | | | | => 1
TRACE t431: | | | | | | | | | => 1
TRACE t430: | | | | | | | | => 2
TRACE t429: | | | | | | | => 6
TRACE t428: | | | | | | => 24
TRACE t427: | | | | | => 120
TRACE t426: | | | | => 720
TRACE t425: | | | => 5040
TRACE t424: | | => 40320
TRACE t423: | => 362880
TRACE t422: => 3628800
3628800
```
Kelihatan perbedaannya, ngga?
Jadi gimana cara kerja recursion?
Jadi gimana cara kerja function?
