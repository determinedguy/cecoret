---
layout: post
title: Modularisasi pada Flutter
categories: [Flutter, PBP]
---

Bayangin nih, kamu lagi ngembangin suatu aplikasi dengan arsitektur monolitik. Mungkin awalnya biasa aja kali ya, soalnya kamu ngembanginnya sendiri atau sama kelompok kecil gitu. Nah tapi, apa yang terjadi kalau aplikasi buatan kamu semakin berkembang dan memiliki banyak fitur? Pusing dong ya gak ya; banyak fitur yang harus dikembangin dan dipertahanin, kali aja kalau rekrut orang lebih malah berarti makin banyak yang ngurusin aplikasi kamu .... 😫

### Noh, pusing gak?

> Here comes the modular concept~

#### Modularisasi? Apaan tuh? 🤔

"Modularisasi adalah teknik untuk memecah suatu sistem dari yang awalnya satu proyek monolitik menjadi beberapa modul yang terpisah dan independen."

Bayangin (lagi-lagi), aplikasi yang kamu kembangkan udah besar skalanya dan sementara masih pakai arsitektur monolitik (intinya semua kode ditaruh di modul yang sama, nggak dipisah gitu). Kalau masih maksa pakai arsitektur monolitik, nanti ribet; bayangin ada kode terus seharian nyari *error*-nya nggak ketemu-ketemu, terus ternyata *error*-nya gegara ada pengembang lain yang nggak sengaja nimpa kode yang baru saja kamu tambahkan dan malah kode yang udah kamu buat dengan susah payah hilang ditelan `git commit` (wokwokwok kasihan 😂).

Akhirnya kamu coba mikir konsep modularisasi ini ....

#### Apa sih untungnya pake modularisasi ini?

Modularisasi sebenarnya menerapkan konsep *separation of concerns* (SoC) yang intinya menyatakan bahwa setiap orang atau anggota tim dapat fokus pada bagian yang dikerjakannya. Dengan demikian, kita dapat meminimalisisasi konflik yang dapat terjadi dalam perubahan kode.

> Ahay, gak kena timpa git commit lagi dong! 😆

Selain itu, modularisasi bisa buat proses *build* menjadi lebih cepat. Bayangin nih kalau masih keukeuh pake arsitektur monolitik, keseluruhan aplikasi akan dikompilasi dan dibangun ulang saat ada perubahan kode; mau sekecil apapun itu! Kan kasihan komputernya; udah *racing mode* gegara Flutter (*insert fan noise here NGUENGGG*) terus disuruh *build* aplikasi dari awal, gak capek apa tuh?

Nah kalau aplikasi kita udah pake arsitektur modular, maka hanya modul yang memiliki perubahan kode sajalah yang akan di-*build* ulang; canggih!

Manfaat utama terakhir dari modularisasi adalah mudahnya penggunaan kembali (*reusability*) modul pada modul atau aplikasi lain. Misalnya nih, kamu punya modul buat nanganin permintaan ke peladen Django, terus kamu buat aplikasi baru, udah deh tinggal pakai ulang modul yang dulu pernah dibuat. 💡

### Tapi, kapan sih baiknya pakai konsep ini?

Pastinya nggak semua aplikasi harus dikembangkan pakai arsitektur modular. Misal, sebuah aplikasi sederhana dengan dua halaman statik; tentunya kurang bermanfaat kalau kita maksa aplikasinya dimodularisasi.
