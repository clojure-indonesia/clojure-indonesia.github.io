---
layout: post
title:  "Threading Macros"
date:   2024-04-04 10:26:00 +0700
---
Do you know what LISP stands for?
- Lots of Insipid, Stupid Parentheses
- Lots of Irritating Superfluous Parentheses

🙈😂🏃 dan masih banyak lagi; kepanjangannya entah untuk lucu-lucuan, entah untuk mengerdilkan tidak penting (tersinggung itu pilihan), dan lispers nerima aja dikatain begitu. Menurut lispers, parentheses adalah fitur, bukan bug; (you should deal with it, bet with it, be adaptive).
```cl
CL-USER> (let ((greet "Halo")
               (city "Bandung"))
           (concatenate 'string greet ", " city))
"Halo, Bandung"
```
Ah! my eyes, lihat tanda kurung itu--All hail Common LISP! Munculnya Clojure juga mencoba mengurangi penggunaan tanda kurung--sedikit--karena Clojure masih tetap menggunakan _prefix notation_, masih dengan _parentheses_.
```clj
user> (let [greet "Halo"
            city "Bandung"]
        (str greet ", " city))
"Halo, Bandung"
```
Sedikit lebih baik? Clojure? Iya--tapi kan ekspresinya simpel, tanda kurung kan ngeganggu kalo ekspresinya banyak, ambil contoh 5:
```clj
user> (keyword (clojure.string/capitalize (clojure.string/replace (clojure.string/reverse (str 'abc)) "c" "d")))
:Dba
```
```clj
user> (keyword
       (clojure.string/capitalize
        (clojure.string/replace
         (clojure.string/reverse (str 'abc))
         "c"
         "d")))
:Dba
```
Gimana? 🙈😂🏃; Clojure nyoba lagi ngurangin tanda kurung seperti di atas lewat macro, `->` (thread-first) dan `->>` (thread-last).
```clj
user> (-> 'abc
          str
          clojure.string/reverse
          (clojure.string/replace "c" "d")
          (clojure.string/capitalize)
          keyword)
:Dba
```
Way better, tapi gimana cara memahami `->` (thread-first), kalo aku bisa dimulai dengan baca dokumentasi dari Clojure:
```clj
user> (doc ->)
-------------------------
clojure.core/->
([x & forms])
Macro
  Threads the expr through the forms. Inserts x as the
  second item in the first form, making a list of it if it is not a
  list already. If there are more forms, inserts the first form as the
  second item in second form, etc.
nil
```
Dari dokumentasi di atas bisa kita mapping:
- Masukkan `x` -> `'abc` sebagai item kedua pada `form pertama` -> `str` 
- Bikin jadi list--kalo dia belum list -> `str` belum list--belum ada tanda kurungnya, dibikin jadi list `(str 'abc)`
- Kalo forms-nya banyak, masukkan `form pertama` -> `(str 'abc)` sebagai item kedua pada `form kedua` -> `clojure.string/reverse` jadinya `(clojure.string/reverse (str 'abc))`
- Begitu seterusnya 🙈😂🏃

Coba kita bikin juga yang `->>` (thread-last):
```clj
user> (vec (map (fn [n] (* n 5)) (filter odd? (map inc (range 10)))))
[5 15 25 35 45]
```
```clj
user> (->> (range 10)
           (map inc)
           (filter odd?)
           (map (fn [n] (* n 5)))
           vec)
[5 15 25 35 45]
```
Return-nya sama, ekspresinya sedikit berbeda; `->` dan `->>` sangat membantu--mempermudah saat membaca ekspresi (proses); ini dokumentasinya, coba bikin mappingnya 🙈😂🏃
```clj
user> (doc ->>)
-------------------------
clojure.core/->>
([x & forms])
Macro
  Threads the expr through the forms. Inserts x as the
  last item in the first form, making a list of it if it is not a
  list already. If there are more forms, inserts the first form as the
  last item in second form, etc.
nil
```
Aku percaya tanda kurung adalah fitur, bukan bug, buktikan aku salah! 🙈😂🏃
