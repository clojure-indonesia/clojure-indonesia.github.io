---
layout: post
title:  "Melihat dengan macroexpand"
date:   2024-01-23 09:01:00 +0700
---

Clojure, oh, tidak hanya Clojure--LISP cukup sering dijumpai dengan istilah: `almost no syntax`, kenapa? apa menariknya bahasa pemrograman yang hampir `tidak mempunyai syntax`?, jawaban kenapa memang lebih baik melalui pengalaman, merasakan, menuliskan banyak `()`--alasan yang mungkin bisa dipakai tanpa memahami: karena LISP muncul dengan `core` yang sangat simpel, oh sorry, kecil; simpel bisa jadi perdebatan secara arti karena arti simpel sangat subjektif, tergantung siapa. 

Dengan hampir tidak adanya syntax, bahasa pemrogramaan diharapkan stabil, `tidak berkembang`; programmer tidak perlu menghapalkan setiap `construct`--setiap muncul versi baru; programmer tidak perlu mencari `cara terbaik menggunakan construct`, fokus saja mencari cara terbaik menyelesaikan masalah yang memang layak untuk diselesaikan, sebagai contoh aku pakai `Scheme` dan `Clojure` untuk task yang tidak penting sebetulnya:

#### Scheme:
```scheme
(define (++ a b)
  (if (null? a)
    b
    (cons (car a) (++ (cdr a) b))))
```

#### Clojure:
```clojure
(defn ++ [a b]
  (if (empty? a)
    b
    (cons (first a) (++ (rest a) b))))
```

Sama aja ya kan, Scheme pertama kali muncul 1975, Clojure pertama kali muncul 2007, kemana aja? apakah teknologi tidak berkembang? teknologi berkembang sedikit ngga ngaruh--teknologi berkembang kok setiap hari, `sedikit-sedikit`, tapi konsepnya, corenya, masih sama! (ini menyimpang sekali).

Sekarang coba kita lihat dalemannya dengan `macroexpand` di Clojure:
```clojure
(macroexpand '(defn ++ [a b]
               (if (empty? a)
                 b
                 (cons (first a) (++ (rest a) b)))))
```
dan hasilnya adalah:
```clojure
(def
  ++
  (clojure.core/fn
    ([a b] (if (empty? a) b (cons (first a) (++ (rest a) b))))))
```
Gimana menurutmu?
