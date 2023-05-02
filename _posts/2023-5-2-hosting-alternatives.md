---
layout: post
title: Bahas Hosting (Lagi)
categories: [PBP, Django, Hosting]
---

## Nggak capek apa, Thal?

Tentu saja tidak, dong!

Dengan perkembangan teknologi dan rasa frustasi terhadap batasan yang ada pada [Railway](https://railway.app/) saat mengembangkan aplikasi Django (ingat [artikel ini](https://determinedguy.github.io/cecoret/heroku-to-railway/)?), aku "iseng" mencari alternatif PaaS yang dapat mendukung aplikasi Python (khususnya Django); "ya kali aja ada kan," pikirku.

### Eh, tahunya beneran ada dong!

Aku menemukan dua alternatif yang ke depannya mungkin dapat dijadikan sarana pengembangan aplikasi 😉. Sebenarnya, aku menemukan banyak alternatif yang sudah tersedia cukup lama dan kelihatannya cukup menarik. Sayangnya kebanyakan layanan bersifat BYOC (*Bring Your Own Cloud*), sehingga layanan tersebut hanya bertindak sebagai *middleware* antara kita sebagai pengembang aplikasi dengan *cloud platform*; bisa dianggap mengambil peran DevOps dalam proses pengembangan aplikasi.

1. [DOM Cloud Hosting]

    [DOM Cloud Hosting] merupakan PaaS yang dibuat oleh [Wildan Mubarok](https://wellosoft.net/) (*Orang Indonesia, cuy!*). Beliau sendiri membuat layanan [DOM Cloud Hosting] karena beliau juga frustasi dengan terbatasnya layanan *hosting* gratis yang dapat digunakan untuk tugas perkuliahan.

    > "We want students, teachers, developers with their hobby time make use of our platform for a better experience with putting things online. Personally, the reason I created this because I once struggled to find a host service that's good enough for a university project."
    >
    > Sumber: [Our Philosophy - DOM Cloud](https://domcloud.co/docs/intro/philosophy)

    Secara garis besar, layanan gratis yang diberikan oleh [DOM Cloud Hosting] sendiri cukup menggiurkan; kapasitas sebesar 1.5 GB untuk 3 situs web, domain `*.domcloud.io` gratis, dan sertifikat SSL gratis dengan layanan [Let's Encrypt](https://letsencrypt.org/).

    ![Contoh Dashboard](https://i.ibb.co/TwbSTwD/Screenshot-2023-05-02-06-13-05.jpg)

    Sayangnya [DOM Cloud Hosting] belum memiliki dokumentasi yang cukup memadai, mengingat layanan ini hanya dikembangkan oleh seorang saja. Beberapa templat konfigurasi (dalam bentuk YAML) sudah disediakan, namun kamu tetap perlu mengerti fungsinya masing-masing agar kamu dapat mengkustomisasi konfigurasi agar cocok dengan konfigurasi aplikasimu.

    Apabila kamu mau mengembangkan aplikasi dari awal, [DOM Cloud Hosting] telah menyediakan beberapa templat aplikasi, seperti Wordpress, Laravel, Express, Django, Flask, dan lain-lain.

    Aku akan coba untuk mencontohkan bagaimana cara mengimpor aplikasi Django yang sudah dibuat sebelumnya (untuk Heroku dan Railway, uhuk!) untuk dijalankan di [DOM Cloud Hosting].

    1. Buka situs web [DOM Cloud Hosting] dan lakukan [registrasi akun](https://my.domcloud.co/login). Kamu dapat menggunakan akun surel biasa, GitHub, atau Google.

        ![Login](https://i.ibb.co/JqZtNtq/Screenshot-2023-05-02-09-58-10.jpg)

        ![Register](https://i.ibb.co/CHDvzmK/Screenshot-2023-05-02-09-58-19.jpg)

    2. Setelah registrasi, login dan tekan tombol `Add a website`.

    3. Kamu dapat memilih untuk menggunakan templat yang sudah disediakan (`Start from Template`), mengimpor repositori GitHub yang sudah ada (`Clone from GitHub`), atau mengkustomisasi skrip templat *deployment* sendiri. Kita akan memilih opsi impor repositori GitHub (`Clone from GitHub`).

        ![Halaman Awal 1](https://i.ibb.co/LkdJQLb/Screenshot-2023-05-02-08-36-08.jpg)

        ![Halaman Awal 2](https://i.ibb.co/Mntt9dD/Screenshot-2023-05-02-08-36-19.jpg)

    4. Jika kamu belum memperbolehkan layanan untuk mengakses GitHub-mu, silakan berikan akses kepada layanan agar repositori aplikasimu dapat muncul sebagai pilihan repositori yang ingin diimpor.

    5. Pilih repositori aplikasi yang ingin kamu gunakan. Tautan repositori akan muncul secara otomatis di kode templat aplikasi.

        Berikut adalah contoh konfigurasi *deployment* untuk aplikasi Django yang sudah dibuat sebelumnya. Konfigurasi ini juga menginisiasi layanan PostgreSQL dan sertifikat SSL untuk layanan HTTPS. Jika kamu ingin menggunakan konfigurasi ini, jangan lupa untuk menyesuaikan sumber aplikasi (sesuaikan dengan tautan repositori GitHub aplikasimu) dan nama aplikasi (dalam contoh di bawah, nama aplikasi Django adalah `reflekt_io`) agar proses *deployment* aplikasimu dapat berjalan dengan lancar dan kamu tidak perlu mengulang proses *deployment* karena adanya kesalahan konfigurasi.

        ```yaml
        features:
          - python
          - postgresql
          - ssl
        source: 'https://github.com/reflekt-io/reflekt.io-domcloud'
        root: public_html/public
        nginx:
          ssl: always
          passenger:
            enabled: 'on'
            # Run Python by Phusion Passenger from pyenv
            python: .pyenv/shims/python
        commands:
          - 'pip install -r requirements.txt'
          # Change allowed host config
          - 'sed -i "s/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = \[''${DOMAIN}''\]/g" reflekt_io/settings.py'
          # Initialize middleware between Python (Django) and Phusion Passenger
          - 'echo "from reflekt_io.wsgi import application" > passenger_wsgi.py'
          - 'python manage.py migrate'
          - 'mkdir public'
        ```

    6. Kamu dapat mengubah *username* situs web yang juga akan menjadi domain dari situs web aplikasimu. Kamu juga dapat mengubah wilayah *deployment* aplikasi sesuai keinginanmu (Singapura, New York, atau Prancis). Informasi mengenai kapasitas, data jaringan, dan jumlah layanan web tersisa juga tersedia di bawah.

        > PERHATIAN: Jika kamu akan menghapus proyek ini, jangan gunakan nama yang ingin kamu gunakan sebagai nama situs web final. Kamu tidak akan dapat mengklain nama situs web sebagai domain setelah kamu membuat situs web dengan nama tersebut (atau sudah ada orang lain yang mengklaim nama tersebut).
        >
        > Jika kamu sudah membuat proyek dengan nama yang kamu inginkan, maka jangan hapus proyek jika kamu ingin mengonfigurasi proyek dari awal; ganti saja konfigurasi *deployment* dan sesuaikan daripada menghapus proyek dan kehilangan kesempatan untuk mengklaim nama yang kamu inginkan. Walaupun proyek kamu dihapus, kamu tidak akan dapat mengklaim nama tersebut kembali; *basically it is gone forever*.
        >
        > #pengalaman :(

    7. Ketika kamu sudah siap melakukan *deployment*, tekan tombol `Add Website` untuk memulai proses *deployment*. [DOM Cloud Hosting] akan melakukan proses *deployment* secara otomatis sesuai dengan konfigurasi yang telah kita buat.

    Tada! Seharusnya aplikasimu sudah dapat diakses melalui tautan web yang diberikan oleh [DOM Cloud Hosting]. Jika terdapat *error* pada aplikasi Django-mu, silakan lakukan *troubleshooting* dan *debug* dengan mencari permasalahan yang kamu hadapi di Google dan/atau Stack Overflow.

    Ketika kamu telah berhasil melakukan *deployment*, kamu juga dapat mengonfigurasi *deployment* secara otomatis melalui layanan `Webhook` yang disediakan oleh [DOM Cloud Hosting]. Ketika ada kode yang di-*push* ke dalam GitHub, [DOM Cloud Hosting] akan melakukan *deployment* secara otomatis dengan melakukan perintah yang diberikan di bagian `Webhook`.

    Berikut adalah cara mengatur *deployment* secara otomatis melalui fitur `Webhook`.

    1. Buka proyek aplikasimu dan buka menu `Webhook`.

    2. Pilih repositori GitHub aplikasimu dan sesuaikan status aplikasi. Tentunya kita akan memilih Django sebagai contoh dalam kasus ini.

    3. Kamu akan diberikan templat konfigurasi dengan kode `git pull`. Kamu dapat menggunakan contoh konfigurasi berikut ini sebagai konfigurasi `Webhook` aplikasimu.

        ```yaml
        commands:
          # Use stash to avoid unstaged changes problem
          - git stash
          - git pull
          - git stash pop
        ```

    4. Klik `Add` setelah kamu mengonfigurasi repositori dan status aplikasi.

    Layanan `Webhook` sudah terkonfigurasi. Aplikasi kamu akan diperbarui ketika kamu melakukan *push* ke dalam repositori GitHub aplikasimu.

    Sebagai informasi (2 Mei 2023), domain `*.domcloud.io` belum dapat diakses dengan jaringan UI karena terindikasi sebagai *malware* oleh Palo Alto Networks (layanan *screening* situs web yang digunakan oleh DSTI UI). Informasi ini akan aku perbarui sesaat setelah terdapat informasi lanjutan.

    ![Informasi Blokir](https://i.ibb.co/VWb8LFD/Screenshot-2023-05-02-09-48-43.jpg)

2. [Adaptable]

    Tidak banyak informasi latar belakang yang dapat digali dari Internet mengenai [Adaptable] selain "*just connect your GitHub repository and let Adaptable handle the rest*". 🤔

    Layanan gratis yang diberikan oleh [Adaptable] juga tidak kalah dibandingkan PaaS lainnya; *deployment* aplikasi yang *containerized* dan *scalable*, fasilitas basis data terkelola (MongoDB dan PostgreSQL), *continuous deployment* dari GitHub, sertifikat SSL/TS gratis, dan *shared app build pool*.

    ![Contoh Dashboard](https://i.ibb.co/6RnKVhP/Screenshot-2023-05-02-00-07-01.jpg)

    Sayangnya, untuk saat ini kamu membutuhkan kode undangan (*invitation code*) untuk menggunakan layanan ini. Namun, kode undangan dapat didapatkan dengan mudah dengan *request* untuk bergabung ke beta melalui tautan yang tersedia pada halaman *Sign up*.

    ![Sign Up Page](https://i.ibb.co/7234nVc/Screenshot-2023-05-02-08-27-46.jpg)

    Selain itu, layanan ini sepertinya masih sangat mengandalkan GitHub untuk autentikasi akun. Hal ini tentunya perlu diperhatikan apabila kamu menggunakan layanan repositori Git selain GitHub.

    Seperti sebelumnya, aku akan coba untuk mencontohkan bagaimana cara mengimpor aplikasi Django yang sudah dibuat sebelumnya untuk dijalankan di [Adaptable].

    1. Buatlah akun terlebih dahulu; yang sabar ya untuk menunggu kode undangannya. 😅

    2. Jika sudah mendapatkan kode undangan, masukkan kode undangan pada kolom input yang tersedia dan tekan tombol `Sign Up with GitHub`.

    3. Jika sudah login, silakan tekan tombol `New App`. Pilih `Connect an Existing Repository`.

    4. Pilihlah repositori aplikasimu sebagai basis aplikasi yang akan di-*deploy*. Pilih *branch* yang ingin dijadikan sebagai *deployment branch*.

    5. Pilihlah templat *deployment* yang sesuai dengan aplikasimu. Tentunya kita akan memilih `Python App Template` sebagai contoh pada kasus ini.

    6. Pilihlah tipe basis data yang akan kamu gunakan untuk aplikasimu. Kita akan memilih `PostgreSQL`.

    7. Sesuaikan versi Python sesuai dengan spesifikasi aplikasimu dan masukkan perintah `python manage.py migrate && gunicorn reflekt_io.wsgi` sebagai `Start Command` untuk proyek aplikasimu. Sesuaikan `reflekt_io` dengan nama proyek aplikasi Django-mu.

    8. Masukkan nama aplikasimu yang juga akan menjadi nama domain situs web aplikasimu.

    9. Centang bagian `HTTP Listener on PORT` dan klik `Deploy App` untuk memulai proses *deployment* aplikasi.

    Tada! Proses *deployment* telah selesai. [Adaptable]—sesuai dengan *tagline*-nya—hanya meminta kita untuk menghubungkan repositori GitHub dengan konfigurasi yang minimum, sisa proses *deployment* dilakukan secara otomatis. Canggih, bukan?

[DOM Cloud Hosting]: https://domcloud.co/
[Adaptable]: https://adaptable.io/
