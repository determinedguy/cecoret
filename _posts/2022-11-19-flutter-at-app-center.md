---
layout: post
title: Using Microsoft Visual Studio App Center to Publish Flutter Applications
categories: [Flutter, PBP]
---

> Disclaimer: I spent seven hours of doing this stuff.

Dengan berlakunya rubrik baru untuk proyek akhir semester pada mata kuliah Pemrograman Berbasis Platform (PBP), aku pun harus mengetes apakah rubrik tersebut *feasible* dikerjakan oleh mahasiswa. Salah satu kriteria yang perlu dipenuhi untuk mendapatkan nilai penuh adalah tersedianya aplikasi untuk diuji melalui [*Firebase App Distribution*](https://firebase.google.com/docs/app-distribution) atau [*Microsoft Visual Studio App Center*](https://appcenter.ms/). Tentunya *release* pada GitHub dengan GitHub Actions tetap perlu dipenuhi di samping kriteria tersebut.

> "Itu mah ez pz; tinggal pake [*script* Actions gue](https://gist.github.com/determinedguy/68b9a39b49099222f7c4b12eb617c643)." —LAH, 2021<br /> *Be careful though, it is a little bit deprecated!*<br /> Versi terbaru akan dijelaskan di bawah.

Dengan adanya keadaan baru ini, aku merasa harus mencoba untuk melakukan kriteria tersebut sebelum rubrik rilis ke publik. ~~Susah kan ya gais soalnya belum pernah ada yang pernah~~ Jadinya kalau kata orang, {% include pullquote.html quote="'PBP is used to be fun, or is it still?'" %} Jujur; awalnya aku takut bahwa hal ini tidak dapat dilakukan oleh kelompok masing-masing dengan diberikannya rentang waktu yang (sebenarnya) cukup singkat dibandingkan dengan beban yang harus dikerjakan. Hal ini merupakan hal baru dibandingkan rubrik tahun sebelumnya yang (aku jalani sebelumnya dan) hanya mengecek apakah terdapat APK pada proyek kelompok (*regardless whether it is published manually or via GitHub Actions*). Sebagai seorang ~~koordinator~~ asisten dosen yang bertanggung jawab, aku mencoba untuk mempublikasikan aplikasi yang (kelompok) aku buat ke *Microsoft Visual Studio App Center*.

## Pengaturan Dasar pada App Center

> "Ini mah kayak tutorial biasanya cuma nggak di [situs web PBP](https://pbp-fasilkom-ui.github.io/ganjil-2023/), gak sih?"

Ya ... emang iya, hehe. 😅

Oke; tanpa basa-basi, mari kita ~~coba~~ laksakanan~

> Oh iya; sebenarnya App Center menyediakan fitur *Analytics*, namun kita tidak akan memakainya kali ini karena Flutter belum didukung secara resmi oleh App Center (baru Kotlin/Java, React Native, Xamarin, dan Unity) ~~dan ribet cuy kalau mau maksa, *I have tried and it didn't work so don't waste your time*~~. Kita akan fokus ke pembuatan dan perilisan aplikasi pada App Center saja ~~untuk memenuhi penilaian rubrik secara sempurna~~.

**Pastikan kamu telah membuat repositori pada organisasi kelompok kamu dan repositori tersebut setidaknya berisi *codebase* dasar Flutter dan *Application ID* aplikasi sudah diubah.**

1. Buatlah akun [App Center](https://appcenter.ms/) menggunakan akun GitHub kamu. Saat melakukan autentikasi pada GitHub SSO, jangan lupa untuk memberikan akses kepada organisasi kelompok kamu dengan menekan tombol `Grant`.

    ![App Center Login](https://i.ibb.co/wzPtQvw/Screenshot-2022-11-19-09-39-01.png)

2. Buatlah organisasi baru dengan mengakses menu *Add new* -> *Add new organization*. Gunakan nama proyek aplikasi kelompok kamu sebagai nama organisasi.

    > Kalau ada teman kamu yang sudah membuat organisasi pada App Center, minta teman kamu undang kamu melalui menu *People* -> *Collaborators* -> *Invite collaborators by email*. Gunakan surel yang kamu pakai untuk akun GitHub.

    ![Dashboard](https://i.ibb.co/N6B952q/Screenshot-2022-11-19-09-41-57.png)

3. Buatlah *slot* aplikasi baru dengan menekan tombol *Add app*.

    ![Add App](https://i.ibb.co/jTQVtZg/Screenshot-2022-11-19-09-44-38.png)

4. Isi nama aplikasi dan ikon aplikasi sesuai desain aplikasi. Kamu tidak perlu memilih tipe rilis. Pilih `Android` sebagai OS dan `Java / Kotlin` sebagai Platform.

    ![App Settings](https://i.ibb.co/4dCbgR0/Screenshot-2022-11-19-09-44-58.png)

5. Buka menu *Distribute* dan buka menu *Groups*.

    ![Groups](https://i.ibb.co/v3BJMSP/Screenshot-2022-11-19-09-49-42.png)

6. Buatlah grup baru dengan menekan tombol tambah. Berikan nama `Public` dan berikan akses publik dengan mengubah *toggle* pada `Allow public access`. Tekan tombol *Create Group* untuk membuat grup baru. Hal ini kita lakukan agar APK yang nantinya dibuat oleh App Center dapat diakses secara publik.

    ![New Group](https://i.ibb.co/6BqpRFk/Screenshot-2022-11-19-10-40-56.png)

Sampai sini, kita sudah melakukan pengaturan dasar pada App Center. Selanjutnya, kita akan melakukan pengaturan skrip dan pengesahan (*sign*) pada proyek aplikasi Flutter.

## Pengaturan Dasar Pengesahan Aplikasi Flutter

Untuk publikasi aplikasi pada App Center, aplikasi Flutter harus ditandatangani atau disahkan menggunakan *key* agar aplikasi yang dirilis dijamin keabsahannya. Oleh karena itu, kita akan membuat *key* untuk aplikasi dan mengaturnya untuk automasi agar skrip CI/CD (baik yang ada pada GitHub Actions dan App Center nantinya) dapat berjalan dengan baik ~~karena hal ini akan menjadi suatu masalah yang *njelimetnya minta ampun gile dah*~~.

> Panduan asli dapat dilihat disini: <https://docs.flutter.dev/deployment/android><br /> Aku akan tetap menjelaskan bagaimana mengesahkan aplikasi Flutter untuk Android, namun ada beberapa hal yang aku modifikasi (hehe).

**Jangan lupa untuk mengaplikasikan logo atau ikon aplikasi ke dalam proyek aplikasi.** Jika kamu belum mengubahnya, ikuti panduan ini: [Adding a launcher icon](https://docs.flutter.dev/deployment/android#adding-a-launcher-icon).

1. Buatlah sebuah *keystore*.

    Untuk pengguna Mac OS atau Linux, jalankan perintah berikut pada Terminal.

    ```bash
    keytool -genkey -v -keystore ~/release-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias release
    ```

    Untuk pengguna Windows, jalankan perintah berikut pada Command Prompt.

    ```batch
    keytool -genkey -v -keystore %userprofile%\release-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias release
    ```

    Perintah ini berguna untuk menyimpan *keystore file* dengan nama `release-keystore.jks` di direktori `home` kamu dengan alias `release`. Pindahkan file tersebut ke dalam *root folder* proyek aplikasi dan tambahkan sintaks berikut pada file `.gitignore` yang ada di *root folder* proyek aplikasi agar *keystore* tidak dihitung masuk sebagai file yang ada di repositori Git.

    ```sh
    # Remember to never publicly share your keystore.
    # See https://flutter.dev/docs/deployment/android#reference-the-keystore-from-the-app
    *.keystore
    *.jks
    ```

2. Buka berkas `/android/app/build.gradle`.

3. Carilah bagian `buildTypes`.

    ```groovy
       buildTypes {
            release {
                // TODO: Add your own signing config for the release build.
                // Signing with the debug keys for now,
                // so `flutter run --release` works.
                signingConfig signingConfigs.debug
            }
        }
    ```

    Ubahlah bagian tersebut menjadi seperti berikut.

    ```groovy
        signingConfigs {
            release {
                    storeFile file("../../release-keystore.jks")
                    storePassword = "$System.env.KEY_PASSWORD"
                    keyAlias = "release"
                    keyPassword = "$System.env.KEY_PASSWORD"
            }
        }
        buildTypes {
            release {
                signingConfig signingConfigs.release
            }
        }
    ```

Sampai sini, kita sudah melakukan pengaturan dasar untuk pengesahan aplikasi. Selanjutnya, kita akan melakukan modifikasi skrip GitHub Actions *(pembuatan, jika belum)* dan pembuatan skrip baru untuk *build* pada App Center.

## Pembuatan Skrip GitHub Actions

1. Hasilkan sebuah `base64` *string* sebagai representasi dari *keystore file* yang akan kita simpan sebagai *environment variable* nantinya.

    Jalankan perintah `openssl base64 -in release-keystore.jks` pada *root folder* untuk menghasilkan `base64` *string*. Tampung *string* tersebut untuk sementara waktu (sebagai contoh, dengan menggunakan Notepad atau Visual Studio Code).

2. Buatlah *repository secrets* pada repositori GitHub dengan spesifikasi sebagai berikut.

    i. `GH_TOKEN` berisi GitHub (Personal Access) Token dari salah satu admin repositori untuk kepentingan *automated release*.

    ii. `KEY_JKS` berisi `base64` *string* dari *keystore file* yang telah kamu buat sebelumnya.

    iii. `KEY_PASSWORD` berisi kata sandi yang kamu gunakan saat kamu membuat *keystore file*.

3. Buka (buat, jika belum ada) folder `.github/workflows`.

4. Buatlah tiga file baru dengan spesifikasi yang ada pada [GitHub Gist ini](https://gist.github.com/determinedguy/16add60b5b347c40b75066665110c7bf).

5. Simpan file tersebut dan *push* ke repositori. Cek apakah aplikasi berhasil dibuat dan dirilis oleh GitHub Actions secara otomatis.

Apabila aplikasi kamu berhasil dibuat dan dirilis otomatis, maka selamat! Sampai sini, kita sudah mengamankan *workflow* pada GitHub. Selanjutnya, kita akan membuat skrip baru unruk *build* pada App Center dan mengonfigurasi aplikasi secara lebih lanjut pada situs web App Center.

## Penambahan Skrip CI/CD untuk App Center

App Center menggunakan *bash script* untuk menjalankan automasi *build* aplikasi (~~agak lain emang dia~~).

1. Buka folder `/android/app`.

2. Buatlah file baru dengan nama `appcenter-post-clone.sh` dan isi file tersebut dengan kode berikut.

    ```bash
    #!/usr/bin/env bash
    # Place this script in project/android/app/

    cd ..

    # fail if any command fails
    set -e
    # debug log
    set -x

    cd ..
    git clone -b beta https://github.com/flutter/flutter.git
    export PATH=`pwd`/flutter/bin:$PATH

    flutter channel stable
    flutter doctor

    echo "Installed flutter to `pwd`/flutter"

    # export keystore for release
    echo "$KEY_JKS" | base64 --decode > release-keystore.jks

    # build APK
    # if you get "Execution failed for task ':app:lintVitalRelease'." error, uncomment next two lines
    # flutter build apk --debug
    # flutter build apk --profile
    flutter build apk --release

    # if you need build bundle (AAB) in addition to your APK, uncomment line below and last line of this script.
    #flutter build appbundle --release --build-number $APPCENTER_BUILD_ID

    # copy the APK where AppCenter will find it
    mkdir -p android/app/build/outputs/apk/; mv build/app/outputs/apk/release/app-release.apk $_

    # copy the AAB where AppCenter will find it
    #mkdir -p android/app/build/outputs/bundle/; mv build/app/outputs/bundle/release/app-release.aab $_
    ```

3. Buka file `/android/app/.gitignore` dan ubahlah file tersebut menjadi berikut. Hal ini dilakukan agar App Center dapat mendeteksi aplikasi sebagai aplikasi Android.

    ```sh
    # add comment for app center
    # gradle-wrapper.jar
    # /gradlew
    # /gradlew.bat
    /.gradle
    /captures/
    /local.properties
    GeneratedPluginRegistrant.java

    # Remember to never publicly share your keystore.
    # See https://flutter.dev/docs/deployment/android#reference-the-keystore-from-the-app
    key.properties
    **/*.keystore
    **/*.jks
    ```

4. Simpan file tersebut dan *push* ke repositori. Pastikan skrip ini dan `.gitignore` yang baru telah ter-*push* sampai ke *branch* `main`.

Setelah selesai membuat skrip, kita akan mengonfigurasi aplikasi pada App Center agar dapat dibuat dan dirilis secara otomatis.

## Konfigurasi Lanjutan pada App Center

1. Buka situs web App Center dan buka proyek aplikasi.

    ![App Dashboard](https://i.ibb.co/bXgRvXw/Screenshot-2022-11-20-01-29-02.png)

2. Buka menu *Build* dan pilih GitHub sebagai servis penyedia repositori aplikasi. Pilihlah repositori aplikasi proyek kelompok kamu.

    ![Build Dashboard](https://i.ibb.co/02pG0zF/Screenshot-2022-11-20-01-28-57.png)

3. Buka *branch* `main` dan klik tombol *Configure*.

    ![Branch Configuration](https://i.ibb.co/mBJr7bc/Screenshot-2022-11-20-01-31-36.png)

4. Ikuti pengaturan berikut.

    ![Configuration 1](https://i.ibb.co/HVjfGYg/Screenshot-2022-11-20-01-32-17.png)
    ![Configuration 2](https://i.ibb.co/4msqRTZ/Screenshot-2022-11-20-01-34-00.png)
    ![Configuration 3](https://i.ibb.co/XYVzxXg/Screenshot-2022-11-20-01-34-11.png)

    Catatan:

    i. Jangan lupa untuk mengganti `KEY_JKS` dan `KEY_PASSWORD` dengan *value* yang sebenarnya.

    ii. Jangan lupa untuk membuat grup `Public` untuk distribusi aplikasi secara publik.

    iii. Salinlah tautan *build badge* dengan format `Markdown` dan tempelkan ke `README.md`.

    ![Badge Configration](https://i.ibb.co/zhgWpy7/Screenshot-2022-11-20-01-35-32.png)

5. Klik tombol `Save & Build` untuk menyimpan konfigurasi dan memulai proses *build* perdana.

> **INGAT!** *Free tier* pada App Center hanya memberikan 1 *build pipeline* per organisasi atau akun, 240 *build minutes* per bulan, dan maksimal 30 menit per *build*. **Harap gunakan kuota yang diberikan <u>dengan bijak</u>.**

Kamu dapat mengecek tautan publik dari publikasi aplikasi pada App Center melalui menu *Distribute* -> *Groups* -> *Public*.

![Public Group](https://i.ibb.co/x1SXKSC/Screenshot-2022-11-20-01-42-12.png)

Berikut adalah contoh tampilan App Center ketika tautan publik dari publikasi apilkasi diakses oleh pengguna.

![App Release](https://i.ibb.co/hc1B7Kn/Screenshot-2022-11-20-02-12-26.png)

## Selesai! Yay~

Setelah menghabiskan waktu tujuh jam *figuring out things* dan seharian menulis dokumen ini (sembari melakukan simplifikasi alur pengerjaan), aku rasa hal ini lumayan *feasible* untuk dilakukan pada pengerjaan proyek akhir semester <u>secara berkelompok</u>. Hal ini menjadi sebuah tantangan dan keunikan sendiri pada mata kuliah PBP di semester ini.

Jika kamu mengalami masalah, coba cek bagian bawah dari *post* ini. 😉

**Semangat mencari cara untuk melakukan publikasi aplikasi pada App Center!**

> Lah iya ya, kalian tinggal baca dokumen ini; hadeh wkwk ...<br /><br /> *...yes that is a joke, thank you very much*. 🫰

## Masalah yang (Mungkin) Dapat Terjadi

1. Gradle-nya ngambek; benerin dulu versinya ya.
2. Kotlin-nya nggak sesuai versinya; lagi-lagi, benerin dulu versinya ya.

### Intinya sih satu; sabar. 😂🙏❤️
