---
layout: post
title:  "Synchronous, Asynchronous"
date:   2024-03-12 12:28:00 +0700
---
Kapan sebuah ~~program~~ function bisa dikatakan synchronous/asynchronous, dan kenapa? _function aja biar kecil, program itu kumpulan banyak proses_.

Menurut KBBI:
- [sin.kron](https://kbbi.kemdikbud.go.id/entri/sinkron)
  - <span style='color: red'>_a_</span> (terjadi atau berlaku) pada waktu yang sama; serentak
  - <span style='color: red'>_a_</span> sejalan (dengan); sejajar; sesuai; selaras
- [a.sin.kron](https://kbbi.kemdikbud.go.id/entri/asinkron)
  - <span style='color: red'>_a_</span> tidak dalam waktu atau kecepatan yang sama; tidak serentak
  
Menurut Dictionary Cambridge:
- [synchronous](https://dictionary.cambridge.org/dictionary/english/synchronous)
  - happening or done at the same time or speed
- [asynchronous](https://dictionary.cambridge.org/us/dictionary/english/asynchronous)
  - not happening or done at the same time or speed

```clj
user> (+ 1 2 3 4 5 6 7 8 9)
45
```
Ekspresi di atas bisa dibaca: `invoke` function `+` dengan argumen `1 2 3 4 5 6 7 8 9`, kita mendapatkan output `45`, sinkron!
<p align='center'><img src="/assets/sync.png"/></p>
Ekspresi yang kita input bisa dikatakan sinkron ketika kita harus menunggu hasil dari ekspresi tersebut, kita ngga bisa input ekspresi lain sebelum ekspresi sebelumnya selesai; belum begitu kelihatan karena proses yang kita input sangat sederhana--akan kelihatan kalau prosesnya lama (ya akibatnya nunggu lama :v); coba proses yang sama kita kasih `Thread/sleep` sebagai simulasi proses yang memakan waktu yang lama.
```clj
user> (do
        (. Thread sleep 10000) ;; tunggu 10 detik :v (ngga bisa ngapa-ngapain!)
        (+ 1 2 3 4 5 6 7 8 9))
45
```
<p align='center'><img src="/assets/async.png"/></p>
Asinkron; tolong, eksekusi ekspresi ini, aku ngga minta hasilnya, nanti mungkin dan hasilnya harus udah ada, atau aku mungkin juga ngga akan peduli lagi, pokoknya eksekusi aja, aku masih mau ngerjain yang lain.
```clj
user> (def a (agent 0))
#'user/a
user> (defn f1
        [c & args]
        (. Thread sleep 10000) ;; sama nih!; tapi ngga bikin nunggu, bisa ngerjain yang lain
        (apply + c args))
#'user/f1
user> @a
0
user> (send a f1 1 2 3 4 5 6 7 8 9)
#<Agent@48882646: 0>
user> @a
0
user> (*)
1
user> (+)
0
user> "hey"
"hey"
user> @a ;; di sini, prosesnya selesai, aku memilih ambil hasilnya
45
```
Lihat gambar!  
Baca kamus!  
Pelotot kode!  
Sesuai ngga?  
Gimana menurutmu?
