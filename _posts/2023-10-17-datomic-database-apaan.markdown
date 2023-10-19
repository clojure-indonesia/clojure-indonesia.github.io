---
layout: post
title:  "Datomic, Database apaan?"
date:   2023-10-17 03:43:25 +0700
---

Sebenarnya udah lama aku pengen cerita soal Datomic, database yang menurutku sangat keren, database yang tidak tergolong sebagai SQL, tidak juga tergolong NoSQL. Pernah sekali dua kali aku ngobrol soal Datomic, ngobrol langsung sama co-worker dan pertanyaan yang bisa mereka kasih ke aku yang sedang berapi-api bercerita tentang Datomic adalah: `Apakah Datomic cepat?`, kalau aku jawab `Ya`, besar kemungkinan pertanyaan lanjutannya adalah: `seberapa cepat?`, dan aku, anak yang tidak pede (tidak sepede orang lain) dan kurang menyukai konklusi tanpa landasan berpikir memilih diam.

Performa aku menyakininya sebagai usaha kolaborasi: ngga sebatas pakai SQL--cepat, pakai Rust--wuz, pakai Zig, jangan pakai Java lambat! dan lain-lain; Konklusi aku menyakininya sebagai bentuk memahami dari dua sisi, kenapa dan kenapa ngga, apa kekurangan dan kelebihannya; Juga sangat penting untuk melihat masalah apa yang coba diselesaikan.

Jadi masalah apa yang coba diselesaikan oleh Datomic:
- Sangat berorientasi aplikasi, maksudnya kita harus melihat aplikasi dan database sebagai satu kesatuan, database tidak eksklusif, dan ketika aplikasi error yang kita perbaiki ya aplikasi, bukan cuma inject/update state/data ke dalam database terus bergaya seolah-olah aplikasi baik-baik saja.
- History, seperti Git, karena untuk membuat keputusan kita butuh fakta-fakta yang tersedia di masa lalu, tapi kenapa system yang kita design masih menggunakan: `UPDATE [table] SET [column] = [value] WHERE [id] = id`; berarti SQL jelek? jangan pakai SQL, jelek! (ah, ini kenapa aku selalu ngga suka konklusi) 
- Kira-kira gimana caranya scaling system dengan SQL?

Kekurangan Datomic yang bikin impresi pertama langsung kureng adalah `Datomic tidak open-source`, dengan itu saja biasanya langsung pada males buat ngecek lebih jauh; sangat dekat dengan Clojure (ini bisa sebagai kekurangan, bisa juga sebagai kelebihan sih) yang mana Datomic memang ditulis menggunakan Clojure.

Udah segitu dulu aja, jam 4 pagi nih, tidur dulu, nanti kan bisa diedit lagi--kalo banyak yang suka nanti bisa kita tulis part 2