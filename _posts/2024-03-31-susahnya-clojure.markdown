---
layout: post
title:  "Susahnya Clojure"
date:   2024-03-31 09:19:00 +0700
---
Apa yang paling susah dan bikin sebel ketika pertama kali belajar Clojure, nyobain Clojure?, dan kenapa? (khususnya yang udah pernah ngoding di bahasa yang terkenal: JavaScript mungkin, Python, atau PHP).

Di JavaScript kita biasa bikin kek gini, di Python dan PHP juga sama, syntaksnya aja berbeda, pada dasarnya mereka sama: bikin nama untuk suatu value--nanti kita bisa panggil nama tersebut untuk mengambil valuenya; *tetapi* value dari nama tersebut bisa diganti-ganti, variabel!
```js
> name = 'John'
'John'
> name
'John'
> name = 'Jane'
'Jane'
> name
'Jane'
```
Pertama aku bilang `name adalah John`, kemudian aku bilang `name adalah Jane`; yang mana yang benar? John atau Jane? atau aku pembohong?

**Clojure ngga ada fasilitas untuk mengubah data seperti di atas!**
```clj
foo> (def name "John")
#'foo/name
foo> name
"John"
```
Aku bilang `name adalah John`, ngga ada yang bisa mengubah itu!
```clj
foo> (def name "Jane")
#'foo/name
foo> name
"Jane"
```
Bisa kok--dengan didefinisikan ulang, sekarang `name adalah Jane`, tapi tetep di situ-situ aja, mutar-mutar--`name` kemudian ngga bisa diubah lagi kecuali didefinisikan ulang--begitu aja terus--itu makanya Clojurian ngga pernah bilang ini variabel, dan memang bukan!; di Clojure ngga ada variabel--_ini yang susah dan bikin sebel ketika pertama kali belajar, nyobain!_, kenapa? _karena terbiasa dengan variabel di bahasa yang terkenal (contoh: JavaScript) seperti di atas._

Selain `def` (global) ada juga `let` (local), tapi tetep sama: **ngga ada fasilitas untuk mengubah data!**
```clj
foo> (let [name "Fred"]
       name)
"Fred"
```
Kalau begitu gimana caranya aku bikin proses yang berguna (katakanlah), kalo aku ngga bisa mengubah data? **function--pake function--harus pake function!**
```
input -> function -> output
```
Misal dengan `name`, aku mau nambahin nama belakang (beda jaman sama Aristotle--dia hidup di era nama belakang belum ditemukan):
```clj
foo> (str name " " "Doe")
"Jane Doe"
```
Apakah proses di atas mengubah name? Tidak, name tetap `Jane`.
```clj
foo> name
"Jane"
```
Aku mau John dan Jane dengan nama belakang Doe, tapi ngga mau input ngetik `(str name " " "Doe")` dua kali, misal. **function!**
```clj
(def kasih-doe (fn [name]
                 (str name " " "Doe")))
foo> (kasih-doe "Jane")
"Jane Doe"
foo> (kasih-doe "John")
"John Doe"
```
Aku mau John dan Jane dan mungkin banyak lagi sampai 12--anggaplah (mungkin lebih), dengan nama belakang Doe, dan ngga mau ngetik `(kasih-doe "John")` 12 kali, aku cuma ngelist nama-namanya aja.
```clj
foo> (map kasih-doe ["Jane" "John" "Phil" "Bryan" "Fred" "Lucy" "Dom" "Trent" "Andy" "Robin"])
("Jane Doe"
 "John Doe"
 "Phil Doe"
 "Bryan Doe"
 "Fred Doe"
 "Lucy Doe"
 "Dom Doe"
 "Trent Doe"
 "Andy Doe"
 "Robin Doe")
```
Aku mau binding dengan hasilnya seperti di atas, dan bisa diakses lewat index (bikin dulu jadi `vector`, biar bisa diakses lewat index):
```clj
foo> (def list-doe *1)
#'foo/list-doe
foo> list-doe
("Jane Doe"
 "John Doe"
 "Phil Doe"
 "Bryan Doe"
 "Fred Doe"
 "Lucy Doe"
 "Dom Doe"
 "Trent Doe"
 "Andy Doe"
 "Robin Doe")
foo> (def vec-doe (vec list-doe))
#'foo/vec-doe
foo> vec-doe
["Jane Doe"
 "John Doe"
 "Phil Doe"
 "Bryan Doe"
 "Fred Doe"
 "Lucy Doe"
 "Dom Doe"
 "Trent Doe"
 "Andy Doe"
 "Robin Doe"]
foo> (vec-doe 0)
"Jane Doe"
foo> (vec-doe 1)
"John Doe"
foo> (vec-doe (rand-int (count vec-doe)))
"Robin Doe"
foo> (vec-doe (rand-int (count vec-doe)))
"Lucy Doe"
```
Mundur ke belakang, coba lihat `name`:
```clj
foo> name
"Jane"
```
Kan!!!  
**function**  
**functional programming**  
**fun**
