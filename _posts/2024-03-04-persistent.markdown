---
layout: post
title:  "Persistent"
date:   2024-03-04 12:15:00 +0700
---
Menurut [KBBI](https://kbbi.kemdikbud.go.id/entri/persisten):
- per.sis.ten /pêrsisten/
  1. <span style='color: red'>_v_</span> terus-menerus; bersinambung
  2. <span style='color: red'>_a_</span> gigih; kukuh
  
Menurut [Dictionary Cambridge](https://dictionary.cambridge.org/dictionary/english/persistent):
- persistent
  1. lasting for a long time or difficult to get rid of
  
Sebelumnya aku coba nulis [Immutability](https://clojure-indonesia.github.io/2024/02/25/immutability.html)--tulisan jelek dan gantung (dan aku ngga peduli)--_Ignorance is bliss_!, tapi kenapa nyoba nulis lagi aku pun ngga tau, pengen aja (menurutku ini alasan yang cukup). Definisi apa `persisten` udah ada, diambil dari KBBI dan Dictionary Cambridge, yang perlu dipelajari adalah kenapa? dan atas dasar apa?

Ketika `my-list` udah dibinding dengan value `(1 2 3)`, maka `my-list` immutable, tidak pernah berubah!, terus bagaimana aku bisa bikin proses yang, _katakanlah menambah nomor 4 ke dalam `my-list`_?
```clj
user> (def my-list '(1 2 3))
#'user/my-list
user> my-list
(1 2 3)
```
*quote* bukan typo! (ha!, ini bisa buat nyoba-nyoba tulisan selanjutnya); sekarang gimana cara menambah `4` ke dalam `my-list`?
```clj
user> (conj my-list 4)
(4 1 2 3)
```
apakah `my-list` berubah?
```clj
user> my-list
(1 2 3)
```
*immutability*!

Dengan pov immutability, _benar_ bahwa `conj` di atas membuat `list` baru tanpa mengubah `my-list` versi awal. Dengan pov persistent, ngga saklek kek gitu (bukan copy `my-list` kemudian tambahkan `4` ke dalamnya)--ini yang bikin kenapa `persisten` menjadi concern di area performa; karena yang sebenarnya terjadi adalah tetap menggunakan `my-list` tanpa copy kemudian menambah value `4`, *bersinambung*.

Buktinya:
```clj
user> (identical? (rest (conj my-list 4))
                  my-list)
true
```
