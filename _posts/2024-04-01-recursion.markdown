---
layout: post
title:  "Recursion"
date:   2024-04-01 19:48:00 +0700
---
Selalu tricky kalo ngomongin `recursion`, selalu berbahaya kalo merasa udah tau (aku mending ngga tau daripada merasa tau). `Recursion--function yang memanggil (invoke) dia sendiri, function yang memanggil (invoke) dia sendiri, function yang memanggil (invoke) dia sendiri.`

Terus kapan dia akan berhenti? Yep, itu dia pertanyaanya, itu dia yang perlu dipahami. Sekarang, coba mana kodenya?
```clj
user> (defn factorial
        [n]
        (if (zero? n)
          1
          (* n (factorial (dec n)))))
#'user/factorial
user> (factorial 10)
3628800
user> (* 1 2 3 4 5 6 7 8 9 10)
3628800
```
Factorial di atas sebagai contoh, dia akan berhenti ketika `n sama dengan 0`, ketika `n tidak sama dengan 0`, dia memanggil dia sendiri dengan proses `n` yang kita bikin untuk selalu mendekati (towards) `0`.

Sebentar, coba kita melipir ke `Common LISP`, Common LISP ada function bawaan--`trace` yang cukup membantu ngasih visualisai recursion, kode di atas (Clojure) coba kita terjemahkan juga ke Common LISP:
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
CL-USER> 
```
Clojure ngga ada function bawaan begitu, kita harus pake library `org.clojure/tools.trace`, tanpa bikin `deps.edn` gini caranya:
```bash
clojure -Sdeps '{:deps {org.clojure/tools.trace {:mvn/version "0.8.0"}}}'
```
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
Coba pake angka yang besar, 100 mungkin, atau 1000, gimana hasilnya, dan kenapa? coba di`solve` error yang terjadi saat input eksekusi `(factorial 100)`, terus di`solve` juga error yang terjadi ketika eksekusi `(factorial 1000)`.

Have **fun**ctional programming!
