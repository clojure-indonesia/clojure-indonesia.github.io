---
layout: post
title:  "Nyentuh Java/JVM"
date:   2024-04-06 08:48:00 +0700
---
Clojure itu `hosted`, berjalan di atas `host`: 
- Java Virtual Machine
  - [https://github.com/clojure/clojure/](https://github.com/clojure/clojure/)
- Microsoft .NET
  - [https://github.com/clojure/clojure-clr/](https://github.com/clojure/clojure-clr/)
  - [https://github.com/dmiller/clojure-clr-next](https://github.com/dmiller/clojure-clr-next)
- Browser
  - [https://github.com/clojure/clojurescript/](https://github.com/clojure/clojurescript/)

Apa yang dimaksud dengan `berjalan di atas host`? Sederhana sebenarnya, program yang ditulis (dalam bahasa apapun) perlu dijalankan--dijalankan di mana? Mungkin kalo di 90-an (C, machine code), 2000-an bytecode (JVM, .NET). Siapa yang mendikte program akan dijalankan di mana? client, pengguna programnya lah 🙈😂🏃

Kenapa bytecode? Beberapa programmer sudah tidak peduli--pengennya peduli sama kompleksitas domain, programmer sudah tidak peduli dengan `malloc/free`--kompleksitas domain-nya sudah susah, ditambah kompleksitas tools yang digunakan--tidak menyenangkan.

Di luar itu ada kuot yang cakep sekali dari penulis `Cosmos, Carl Sagan`:
```
If you wish to make an apple pie from scratch, you must first invent the universe.
```

Berarti kalo Clojure berjalan di atas JVM, Clojure adalah Java? Oops, ngga saklek begitu, ada banyak--mungkin ratusan bahasa yang targetnya berjalan di atas Java? Apakah mereka semua Java? Haskell yang berjalan di atas JVM, [Frege](https://github.com/Frege/frege)--apakah dia Java? Haskellian mungkin bisa ngejelasin 🙈😂🏃
```
Java sebagai platform (Java Virtual Machine) berbeda dengan Java sebagai bahasa pemrograman!
```
Dengan berjalan di atas platform, maka dia punya keuntungan, leverage, yang ada di platform tersebut--sebagai contoh, Clojure menggunakan Garbage Collector-nya Java, Clojure punya banyak library (dia bisa pake semua library JVM + library yang ditulis di Clojure).

Coba gimana cara manggil Java di Clojure (kita bikin [ArrayList](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html)):
```clj
user> (def al (java.util.ArrayList.))
#'user/al
user> al
[]
user> (.add al "Jkt")
true
user> al
["Jkt"]
user> (.add al "Bdg")
true
user> (.add al "Sby")
true
user> al
["Jkt" "Bdg" "Sby"]
user> (type *1)
java.util.ArrayList
```
Kalo mau akses item yang ada di ArrayList gimana?
```clj
user> (.get al 0)
"Jkt"
user> (.get al 1)
"Bdg"
```
Edit item yang ada?
```clj
user> (.set al 1 "Mdn")
"Bdg"
user> al
["Jkt" "Mdn" "Sby"]
```
Lho, dia ngga immutable? ya ngga dong, ini data strukur Java, bukan data struktur Clojure! 🙈😂🏃  
Kalo mau hapus semua item di ArrayList
```clj
user> (.clear al)
nil
user> al
[]
```
Clojure ngga berusaha bikin Java lebih baik, seperti Scala, Groovy, dan Kotlin; Pendekatan Clojure adalah bikin bahasa dengan model pemrograman yang unik dan sudah ditatar jaman (LISP) yang berinteraksi dengan baik dengan ekosistem Java.

That's it!
