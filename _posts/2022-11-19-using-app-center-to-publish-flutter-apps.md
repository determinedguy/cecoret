---
layout: post
title: Using Microsoft Visual Studio App Center to Publish Flutter Applications
categories: [Flutter, PBP]
---

Dengan berlakunya rubrik baru untuk proyek akhir semester pada mata kuliah Pemrograman Berbasis Platform (PBP), aku pun harus mengetes apakah rubrik tersebut *feasible* dikerjakan oleh mahasiswa. Salah satu kriteria yang perlu dipenuhi untuk mendapatkan nilai penuh adalah tersedianya aplikasi untuk diuji melalui [*Firebase App Distribution*](https://firebase.google.com/docs/app-distribution) atau [*Microsoft Visual Studio App Center*](https://appcenter.ms/). Tentunya *release* pada GitHub dengan GitHub Actions tetap perlu dipenuhi di samping kriteria tersebut.

> "Itu mah ez pz lemon squeeze; tinggal pake script [GitHub Actions gue](https://gist.github.com/determinedguy/68b9a39b49099222f7c4b12eb617c643)." —LAH\ *Be careful, it's a bit deprecated!*

Dengan adanya keadaan baru ini, aku merasa harus mencoba untuk melakukan kriteria tersebut sebelum rubrik rilis ke publik. Jadinya kalau kata orang, {% include pullquote.html quote="'PBP used to be fun, or is it still?'" %} Jujur; awalnya aku takut bahwa hal ini tidak dapat dilakukan oleh kelompok masing-masing dengan diberikannya rentang waktu yang (sebenarnya) cukup singkat dibandingkan dengan beban yang harus dikerjakan. Hal ini merupakan hal baru dibandingkan rubrik tahun sebelumnya yang (aku jalani sebelumnya dan) hanya mengecek apakah terdapat APK pada proyek kelompok (*regardless whether it is published manually or via GitHub Actions*). Sebagai seorang (~~koordinator~~) asisten dosen yang bertanggung jawab, aku pun mencoba untuk mempublikasikan aplikasi yang (kelompok) aku buat ke *Microsoft Visual Studio App Center*.

## Pengaturan Dasar pada App Center

> "Ini mah kayak tutorial biasanya cuma nggak di [situs web PBP](https://pbp-fasilkom-ui.github.io/ganjil-2023/), gak sih?"

Ya ... emang iya, hehe. 😅

Oke; tanpa basa-basi, mari kita ~~coba~~ laksakanan~

> Oh iya, sebenarnya App Center menyediakan fitur *Analytics*, namun kita tidak akan memakainya kali ini karena Flutter belum didukung secara resmi oleh App Center (baru Kotlin/Java, React Native, Xamarin, dan Unity) ~~dan ribet cuy kalau mau maksa, *I have tried and it didn't work so don't waste your time*~~. Kita akan fokus ke pembuatan dan perilisan aplikasi pada App Center saja ~~untuk memenuhi penilaian rubrik secara sempurna~~.

**Pastikan kamu telah membuat repositori pada organisasi kelompok kamu dan repositori tersebut setidaknya berisi *codebase* dasar Flutter.**

1. Buatlah akun App Center menggunakan akun GitHub kamu. Saat melakukan autentikasi pada GitHub SSO, jangan lupa untuk memberikan akses kepada organisasi kelompok kamu dengan menekan tombol `Grant`.

2. Buatlah organisasi baru dengan mengakses menu *Add new* -> *Add new organization*. Gunakan nama proyek aplikasi kelompok kamu sebagai nama organisasi.

    > Kalau ada teman kamu yang sudah membuat organisasi pada App Center, minta teman kamu undang kamu melalui menu *People* -> *Collaborators* -> *Invite collaborators by email*. Gunakan surel yang kamu pakai untuk akun GitHub.

3. Buatlah *slot* aplikasi baru dengan menekan tombol *Add app*.

4. Isi nama aplikasi dan ikon aplikasi sesuai desain aplikasi. Kamu tidak perlu memilih tipe rilis. Pilih `Android` sebagai OS dan `Java / Kotlin` sebagai Platform.

5. Buka menu *Distribute* dan buka menu *Groups*.

6. Buatlah grup baru dengan menekan tombol tambah. Berikan nama `Public` dan berikan akses publik dengan mengubah *toggle* pada `Allow public access`. Tekan tombol *Create Group* untuk membuat grup baru. Hal ini kita lakukan agar APK yang nantinya dibuat oleh App Center dapat diakses secara publik.

Sampai sini, kita sudah melakukan pengaturan dasar pada App Center.

### bentar dulu ya, aku capek :"
