---
layout: post
title:  "Halo, Dunia!"
date:   2023-10-10 14:02:00 +0700
---

Okay, postingan pertama nih! (postingan pertama yang udah terlalu banyak diedit), apaan Clojure? kenapa Clojure? kenapa ngga Clojure? mungkin kapan-kapan akan coba aku tulis; postingan ini baru sebatas menuliskan Hello, World! karena rasanya belum afdal belajar bahasa pemrograman kalo belum bisa menampilkan Hello, World!.

Hello, World! yang mana aku terjemahkan secara paksa ke dalam bahasa Indonesia menjadi Halo, Dunia!, karena belum pede berbahasa Inggris, belum luwes, masih perlu banyak belajar; grammar masih hancur-hancuran, jadi ya udah pake bahasa Indonesia aja dulu.

Tapi sebelum menulis Clojure yang perlu dan harus dilakukan adalah install Java, tidak asing yaa, atau udah kadung kurang suka Java, tidak apa-apa juga; t-tapi kalo nulis belajar Clojure memang harus install Java. Kenapa? Karena Clojure berjalan diatas JVM (Java Virtual Machine).

Install di MacOS:
```zsh
brew install clojure/tools/clojure
```
Install di Linux bisa juga pake brew, tapi aku kurang suka brew di Linux:
```bash
curl -L -O https://github.com/clojure/brew-install/releases/latest/download/linux-install.sh
chmod +x linux-install.sh
sudo ./linux-install.sh
```
Lengkapnya bisa baca di website [di sini](https://clojure.org/guides/install_clojure), setelah install bisa coba dipanggil compilernya di terminal, seharusnya muncul seperti ini, kalo sudah begini seharusnya kita sudah siap untuk menampilkan Halo, Dunia! menggunakan Clojure:
```bash
~ $ clj --version
Clojure CLI version 1.11.1.1413
~ $ 
```
Yey tinggal menampilkan Halo, Dunia! dengan Clojure  
Kita pake REPL (ketik `clj` di terminal kemudian `Enter`):
```bash
~ $ clj
Clojure 1.11.1
user=> 
```
`user=> ` adalah perintah yang akan kita input, kemudian dibawahnya kembalian dari apa yang kita input, kita tulis `"Halo, Dunia!"`, maka kembaliannya `"Halo, Dunia!"`
```clojure
user=> "Halo, Dunia!"
"Halo, Dunia!"
```
Membuat function bernama `halo` yang akan mengembalikan `Halo, Dunia!` menggunakan `defn`:
```clojure
user=> (defn halo   
         []
         "Halo, Dunia!")    
#'user/halo
user=> (halo)
"Halo, Dunia!"
```
Membuat symbol bernama `halo-dunia-pake-lambda` yang isinya adalah `function` yang mana `function` itu akan mengembalikan `Halo, Dunia!`:
```clojure
user=> (def halo-dunia-pake-lambda
         (fn []
           "Halo, Dunia"))
#'user/halo-dunia-pake-lambda
user=> (halo-dunia-pake-lambda)
"Halo, Dunia"
```
Menggunakan _syntactic sugar_ `lambda` dan beberapa `function` built-in Clojure:
```clojure
user=> (#(apply str %&) "Halo, " "Dunia!")
"Halo, Dunia!"
```
Terakhir yak  
Halo, Dunia!  
Apa kabar Indonesia?  
Semoga kamu lebih baik, baik-baik saja! 