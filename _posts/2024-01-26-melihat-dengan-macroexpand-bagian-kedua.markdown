---
layout: post
title:  "Melihat dengan macroexpand bagian kedua"
date:   2024-01-26 08:12:00 +0700
---

`C` ada fitur `macros`, LISP ada fitur `macros`, dimana keduanya berbeda sekali, penamaan saja yang sama, (ngasih nama emang pekerjaan yang berat), bedanya di mana? kenapa? nanti kapan-kapan coba aku tulis (kalo ngulik C lagi, ngga janji).

1. Kenapa `construct` tidak menjadi primadona di LISP?  
2. Kenapa creator LISP tidak bikin bahasanya kaya akan `construct`?  
3. Kenapa `less is more`?

Aku coba jawab nomor 1 aja, aku pake Clojure--dialek LISP yang aku suka sekali, utamanya fitur immutability (hah, ini ngga nyambung, cuma ngelebarin topik, kapan-kapan aja). Ambil contoh flow-control `when`, `when` adalah `if` dengan hanya `then`--tanpa `else`, (kodenya mana dong):
```clojure
user> (when true 1)
```
`1` akan menjadi kembalian kode di atas, cobain eksekusi di REPL kalau tidak percaya. coba juga kalau `true` diganti `false`:
```clojure
user> (when false 2)
```
kira-kira apa kembaliannya? jawabannya gampang, karena sudah jelas `when` adalah `if` dengan hanya `then`--tanpa `else`, buktinya bisa kita gunakan `macroexpand` di REPL, seperti di bawah:
```clojure
user> (macroexpand '(when true 1))
(if true (do 1))
user> (macroexpand '(when false 1))
(if false (do 1))
```
andai kata `when` tidak diinclude oleh author sebuah bahasa, bisa tidak kita bikin `construct` sendiri seperti `when`? atau harus nunggu author seperti Sun dengan Java, bikin isu di repo public (kalau open source), atau kita bisa bikin `construct` sendiri? Segitu dulu, tolong jawab sendiri, aku mau nyangkul sawah, nanti kulanjutin lagi.
