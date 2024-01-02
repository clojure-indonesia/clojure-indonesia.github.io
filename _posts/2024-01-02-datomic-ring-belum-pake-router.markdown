---
layout: post
title:  "Datomic + Ring, tapi belum pake router"
date:   2024-01-02 18:04:00 +0700
---

Ini mungkin bakal jadi postingan pertama untuk tahun 2024, setelah lama ngga bikin, ngga belajar nulis, kebetulan aku sok sibuk di real life, jaga durian untuk pertama kali setelah beberapa tahun merantau (kurang lebih 12 tahun), tentu ini juga bakal jadi postingan pertama selama di kampung, selain karena sibuk jaga durian kampungnya juga jauh sekali, susah sinyal (waktu nulis ini udah 4G sih, dari EDGE loncat jadi 4G yang baru dibangun akhir tahun 2023 kemarin--grateful), tahun baru yang beneran ada yang baru, selamat tahun baru btw.

Sudah jangan panjang-panjang, kayak dibaca aja, sesuai judulnya Datomic + Ring, Datomic sejenis database transactional yang akutu suka sekali, kenapa suka? aku punya banyak alesannya, ngga perlu mikirin `connection pooling`, ngga perlu mikir `primary key` dan `foreign key`; okay itu bagian suka, kalo tidak suka? hmm... `dia berjalan di atas JVM` (walopun bagian ini aku tetep suka, beberapa orang tidak, tidak apa-apa); apa untungnya ngga mikirin `primary key`? coba ulik sendiri kenapa, biar tulisan ini pendek dan ngga nyimpang kemana-mana.

[Ring](https://github.com/ring-clojure/ring), HTTP server di Clojure, mirip [WSGI](https://wsgi.readthedocs.io/en/latest/), gampangnya kita bikin web service; kalo ngomongin web service sebenarnya kita ngga peduli mau pake apa yang penting kita bisa akses url dan ada kembalian proses seperti biasanya `Hello, World`, atau lebih familiar mungkin Apache, nginx, IIS, dan lain-lain banyak lagi.

Ring di sini hanya sebagai handler, belum termasuk router seperti judul postingan, jadi kita cuma punya satu handler: '/', diikuti `id` yang akan kita cari datanya didalam database:

[https://github.com/clojure-indonesia/ring-datomic/blob/main/src/ring_datomic/core.clj#L51-L52](https://github.com/clojure-indonesia/ring-datomic/blob/main/src/ring_datomic/core.clj#L51-L52), pengambilan `id` yang dikirim dari client (browser, curl, dll):
```clojure
id (-> (replace (:uri request) #"/" "")
       (Integer/parseInt))
```
[https://github.com/clojure-indonesia/ring-datomic/blob/main/src/ring_datomic/core.clj#L57-L62](https://github.com/clojure-indonesia/ring-datomic/blob/main/src/ring_datomic/core.clj#L57-L62), proses query mengambil title by id yang dikirim:
```clojure
(d/q '[:find ?title
       :in $ ?id
       :where [?e :movie/id ?id]
              [?e :movie/title ?title]]
     (d/db conn)
     id)
```
Intinya itu saja sih, tapi kok kodenya panjang? karena kode yang ada di [repo](https://github.com/clojure-indonesia/ring-datomic/blob/main/src/ring_datomic/core.clj) udah sekalian sama proses bikin schema data, dan insert data; databasenya di mana? [https://github.com/clojure-indonesia/ring-datomic/tree/main/db/movies](https://github.com/clojure-indonesia/ring-datomic/tree/main/db/movies)

Segitu aja deh, kepanjangan ini wkwk, bisa baca di [README.md](https://github.com/clojure-indonesia/ring-datomic/blob/main/README.md) atau ngobrol aja di X kalo ada keliru saat `mungkin nyoba`; di sini belum ada fitur komen; [sydney_straya](https://twitter.com/sydney_straya) / [Clojure Indonesia](https://twitter.com/clojure_id)