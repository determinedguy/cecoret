---
layout: post
title: Modularisasi - Teknik Optimasi dan Organisasi pada Flutter
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

Selain itu, modularisasi bisa buat proses *build* menjadi lebih cepat. Bayangin nih kalau masih keukeuh pake arsitektur monolitik, keseluruhan aplikasi akan dikompilasi dan dibangun ulang saat ada perubahan kode; mau sekecil apapun itu!

Kan kasihan komputernya; udah *racing mode* gegara Flutter (*insert fan noise here NGUENGGG*) terus disuruh *build* aplikasi dari awal, gak capek apa tuh? 💔

Nah kalau aplikasi kita udah pake arsitektur modular, maka hanya modul yang memiliki perubahan kode sajalah yang akan di-*build* ulang; canggih!

Manfaat utama terakhir dari modularisasi adalah mudahnya penggunaan kembali (*reusability*) modul pada modul atau aplikasi lain. Misalnya nih, kamu punya modul buat nanganin permintaan ke peladen Django, terus kamu buat aplikasi baru, udah deh tinggal pakai ulang modul yang dulu pernah dibuat. 💡

### Tapi, kapan sih baiknya pakai konsep ini?

Pastinya nggak semua aplikasi harus dikembangkan pakai arsitektur modular. Misal, sebuah aplikasi sederhana dengan dua halaman statik; tentunya kurang bermanfaat kalau kita maksa aplikasinya dimodularisasi.

Nih, coba pertimbangkan poin-poin berikut.

1. Waktu *Build*

    Semakin besarnya ukuran aplikasi karena perkembangannya, maka proses kompilasi dan *build* akan memakan waktu yang sangat lama, bahkan bisa sampai berjam-jam. Tentu kita gak mau bete nungguin mantengin kompilasi sambil dengerin kerasnya kipas ~~angin C_sm_s Wadesta~~ laptop atau komputer yang berusaha tetap buat *everything looks cool* 😎. Nah dengan memakai konsep modular ini, proses kompilasi dan *build* dapat dipersingkat dan diringankan hanya dengan mem-*build* modul yang berubah. 🤟

2. Arsitektur Aplikasi

    Udah dibahas dikit sih tadi ya kan; monolitik sama modular gimana baik-buruknya. Intinya modular lebih baik buat aplikasi yang udah cukup besar, kompleks, dan sulit untuk dikembangkan di satu tempat. Tapi ada kurangnya, nih. Dengan diterapkannya modularisasi, tingkat kompleksitas aplikasi akan bertambah secara signifikan sehingga diperlukan tim atau orang yang bertanggung jawab atas satu modul tertentu. 🤔

    > Cocok sih, buat proyek akhir semester.

3. *Reusability*

    Ketika kita membuat suatu modul, bisa jadi kita tidak hanya menyelesaikan satu solusi yang sedang dikerjakan. Bisa jadi modul yang kita kerjakan adalah fitur umum yang bisa digunakan pada aplikasi lain, contohnya modul autentikasi. Dengan memakai modularisasi, kita bisa menyelesaikan masalah di satu atau beberapa aplikasi dengan hanya mengimpor modul yang telah kita buat sebelumnya. Selain itu, kita juga dapat membuatnya menjadi *open source* lalu mengunggahnya ke *package manager*, seperti `pub`, agar dapat digunakan oleh orang lain sekaligus dikembangkan bersama *developer* lain.

    > Contohnya ya ... [pbp_django_auth](https://pub.dev/packages/pbp_django_auth), hehe.

Udah yakin nih mau lanjut terapin modularisasi? Oke lanjut~

### Eh bentar, modul itu apaan sih sebenarnya?

Pada Flutter, sebuah modul didefinisikan sebagai sebuah *package* atau *plugin*. *Package* dalam Flutter merupakan sebuah paket kode yang ditulis menggunakan bahasa Dart untuk menjalankan sebuah tugas tertentu dan dapat kita tambahkan ke dalam sebuah proyek aplikasi. *Plugin* dalam Flutter merupakan jenis *package* yang spesial karena tidak hanya ditulis dengan Dart, tetapi juga bisa menggunakan Android (Java & Kotlin), iOS (Swift & Objective-C), web, dan desktop.

### Udah ah, buruan ajarin!

Oke, mari kita meluncur ke studi kasus~

Bayangin kamu punya sebuah aplikasi counter sederhana dengan halaman "About Me". Kamu ingin memisahkan halaman "About Me" menjadi sebuah modul sendiri, karena kamu takut ternyata aplikasi ini akan berkembang menjadi sebuah *super app* dengan jumlah pengembang yang ratusan.

![Waduh](https://i.ibb.co/LvQLQFZ/9a24d48eafa6ba090c13cb91bcda5323.jpg)

Awalnya, struktur proyek kamu berupa berikut.

![Struktur Awal](https://i.ibb.co/fQ2X7sR/Selection-2548.png)

Gunakan perintah `flutter create --template=package about` untuk membuat modul dengan nama `about`. Setelah itu, ubah nama file `about.dart` menjadi `about_page.dart` dan pindahkan file tersebut ke dalam folder `about/lib` agar halaman "About Me" berada di dalam modul `about`.

![Struktur Akhir](https://i.ibb.co/xMB2jS2/Selection-2549.png)

Di dalam folder `about`, ternyata ada beberapa berkas untuk konfigurasi *package* (mirip seperti folder proyek Flutter). Kita bisa menambahkan *package* lain sebagai dependensi dari *package* `about` pada berkas `pubspec.yaml`, menuliskan kode uji kasus pada folder `test`, dan menuliskan kode aplikasinya pada folder `lib`.

Setelah kamu memindahkan file halaman "About Me", bisa jadi akan ada error (biasanya terkait *import*). Perbaiki hal tersebut secara manual atau secara otomatis dengan menggunakan bantuan *plugin* Flutter.

Jangan lupa untuk menghapus kode yang tidak dibutuhkan, seperti `about_test.dart` dan kelas `Calculator` di dalam `about/lib/about.dart`.

Setelah membereskan modul `about`, daftarkan *package* ke dalam `pubspec.yaml` milik *main app*.

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  … 
  about:
    path: about
```

Oh iya, kamu sebenarnya dapat mempermudah proses *import package*. Saat ini, kita masih menggunakan impor `AboutPage` secara spesifik.

```dart
import 'package:about/about_page.dart';
```

Isilah file `about/lib/about.dart` dengan kode berikut.

```dart
library about;
 
export 'about_page.dart';
```

Dengan begini, kita cukup mengimpor *package* melalui berkas `about.dart`. Hal ini akan sangat berguna ketika kita nantinya memiliki banyak berkas dalam satu *package*.

```dart
import 'package:about/about.dart';
import 'package:flutter/material.dart';
...
```

Voila! Kamu baru saja menerapkan konsep modularisasi sederhana di Flutter. 😁

Tentunya, kamu dapat menggunakan konsep ini lebih lanjut dengan menerapkan *unit testing* per modul, ekspor modul sebagai *package* yang (siapa tahu) di-*publish* di [pub.dev](https://pub.dev/), dan masih banyak lagi!

### Selamat mencoba! 😆
