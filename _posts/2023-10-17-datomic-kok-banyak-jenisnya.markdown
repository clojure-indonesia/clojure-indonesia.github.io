---
layout: post
title:  "Datomic Pro, Cloud, Local; Kok banyak?"
date:   2023-10-17 11:28:25 +0700
---

Betul, Datomic memang ada 3 jenis:
- Datomic Pro
- Datomic Cloud
- Datomic Local

Datomic Pro nama awalnya adalah Datomic On-Prem (dulu ada Free Starter) terus kemudian ganti nama menjadi Datomic Pro (gratis sejak akhir April 2023, `gratis tetapi tetap tidak open-source`), alasan ganti nama aku ngga tau wkwk, alasan dibikin gratis bisa baca [di sini](https://blog.datomic.com/2023/04/datomic-is-free.html); Datomic Pro cocok untuk mereka yang punya server sendiri, dan mau dan bisa maintain sendiri [https://docs.datomic.com/pro/](https://docs.datomic.com/pro/). Punya server dan mau dan bisa maintain server adalah kombinasi yang `wow`--perlu pertimbangan besar, bisa pun masih sangat luas, bisa--asal jalan atau gimana, keamanan, kalo upgrade apa sistem harus down dulu, dan lain-lain sebagainya. 

Datomic Cloud, sesuai namanya di Cloud (walaupun kalau menurut DHH: `Cloud itu ngga ada, adanya ya sewa server yang di maintain orang lain`; [pencarian DuckDuckGo](https://duckduckgo.com/?q=dhh+cloud&t=brave&ia=web)); Kalo ngga salah Datomic Cloud baru tersedia di AWS, dulunya berbayar di AWS Marketplace, sejak Juni 2023, Datomic Cloud gratis--`gratis tetapi tetap tidak open-source`; Selain itu Datomic juga menyediakan tools yang membantu memanage hampir semua service yang tersedia di AWS, namanya [Ions](https://docs.datomic.com/cloud/ions/ions.html), membantu developer supaya tetap fokus pada pengembangan aplikasi, bukan sibuk konfigurasi service AWS yang entah berapa banyak, entah. [https://docs.datomic.com/cloud/](https://docs.datomic.com/cloud/)

Datomic Local, awal namanya kalo ngga salah Datomic Client, ini cocok untuk mereka yang mau langsung nyoba Datomic, nulis query, langsung crafting, tanpa perlu config banyak, nanti databasenya disimpan seperti folder biasa saja, cocok juga untuk CI [https://docs.datomic.com/cloud/datomic-local.html](https://docs.datomic.com/cloud/datomic-local.html).

Nah, kalo mau lihat CRUD yang sudah jadi, eh bukan CRUD (aku udah ngga mau bilang CRUD wkwk); `ARAR`--Assert, Read, Accumulate, Retract, bisa main ke [sini](https://github.com/clojure-indonesia/pedestal-datomic), di sana ada langkah-langkah singkat--bukan singkat--kasar (tidak user-friendly), dari mulai setup storage--Postgre, bikin database, bikin schema, baca schema dan fakta via [console](https://docs.datomic.com/pro/other-tools/console.html), dan lain-lain, sampai API bisa dihit via cURL; semuanya Clojure tentu saja (aku suka sekali Clojure).