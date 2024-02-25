---
layout: post
title:  "Immutability"
date:   2024-02-25 09:34:00 +0700
---
Apa itu `immutability`? Immutability adalah `sesuatu` yang tidak pernah berubah--tidak diperbolehkan berubah, seperti di Clojure ketika kita nyatakan `my-name = "syd"`
```clojure
(def my-name "syd")
```
maka value dari `my-name` tidak akan pernah berubah, selamanya! (kalau cukup culas, bisa sih--dengan dinyatakan ulang):
```clojure
(def my-name "another name")
```
tapi kalo begini intensinya kan jadi berbeda ya! Immutability yang dimaksud adalah `sesuatu` yang ketika sudah dinyatakan tidak akan pernah berubah--tidak diperbolehkan berubah.

Sebagai pembanding kita akan gunakan JavaScript (bahasa yang tidak menganut immutability secara default):
```js
var my-name = "syd"
my-name = "phil" # karena tidak immutable, maka value dari my-name menjadi "phil"
```
Pembohong!!! Katanya `my-name = "syid"`, kok bisa `my-name = "phil"`?

Coba kita mundur ke matematika, `=` (sama dengan) apakah menyatakan hasil atau menyatakan persamaan--persamaan antara `yang di kiri` dengan `yang di kanan`?

Bisa tidak kita nyatakan `2 + 2 = 4` (hasilnya 4)? atau yang benar adalah `2 + 2 = 4` (sama dengan 4); bagaimana kalau misalnya diganti `2 + 2 ≠ 5`? (cuma bisa tanya saja--maklum ilmu matematika aing masih cetek)

Terus gunanya apa? apa menariknya sesuatu tidak bisa berubah--tidak diperbolehkan berubah pada pemrograman?
