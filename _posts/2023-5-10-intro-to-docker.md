---
layout: post
title: Efisiensi Pengembangan Perangkat Lunak dengan Docker - Sebuah Perkenalan
categories: [Proyek Perangkat Lunak, Software Engineering, Kuliah]
---

Siapa sih yang nggak pernah dengar Docker? Kebanyakan dari kalian pasti sering mendengarnya, namun kalian tidak tahu apa sih yang dimaksud dari Docker. "Makanan kah? Minuman kah? Framework kah?" Hmm.

## Apa sih Docker itu?

Docker adalah sebuah solusi *open-source* yang memungkinkan adanya isolasi aplikasi dan dependensinya ke dalam wadah (kontainer) yang dapat dipindahkan antarlingkungan. Docker yang dibangun dengan bahasa Go ini memisahkan aplikasi dari infrastruktur sehingga kamu dapat mengirimkan perangkat lunak dengan cepat. Keuntungan utama dari kontainer Docker adalah portabilitas dan konsistensi lingkungan, yang memastikan aplikasi dapat berjalan dengan baik di berbagai sistem. Dengan Docker, kamu dapat mengelola infrastruktur dengan cara yang sama seperti mengelola aplikasi. Dengan memanfaatkan metodologi Docker untuk mengirim, menguji, dan men-*deploy* kode dengan cepat, kamu dapat secara signifikan mengurangi penundaan antara menulis kode dan menjalankannya dalam lingkungan *production*.

Kira-kira begini ilustrasi diagram arsitektur Docker.

![Docker](https://docs.docker.com/assets/images/architecture.svg)

## Terus, gimana cara instal Docker?

Caranya sih ... beda-beda ya per sistem operasi :"D

Silakan cek caranya di <https://www.docker.com/get-started> dan ikuti petunjuk instalasi yang disediakan di sana.

## Habis instal, gimana Thal?

Habis instal ... mari kita coba~

Kita akan "bermain" dengan Docker melalui Terminal atau Command Prompt (atau hal-hal sejenisnya, contohnya Powershell), jadi disiapkan ya "mainannya".

Coba jalankan perintah `docker run hello-world`. Apa yang terjadi?

![Docker Hello World](https://storage.googleapis.com/static.configserverfirewall.com/images/docker/docker-hello-world.png)

Perintah di atas akan mengunduh *image* `hello-world` dari Docker Hub (jika belum ada) dan menjalankan kontainer berdasarkan *image* tersebut. Kontainer akan mencetak pesan sederhana sebagai konfirmasi bahwa instalasi Docker berhasil. Kamu juga dapat menentukan opsi tambahan seperti pengaturan nama kontainer, *port mapping*, dan variabel lingkungan dalam perintah `docker run`. Kamu dapat membaca informasi lebih lanjut mengenai `docker run` melalui [Docker Docs](https://docs.docker.com/engine/reference/commandline/run/).

Ah iya, Docker Hub sendiri merupakan repositori Docker *image*. Jadi, kamu dapat menggunakannya untuk membuat kontainer baru berdasarkan aplikasi yang sudah disediakan di sana tanpa repot-repot membuat *image* dari awal. 😉

## Kalau misal aku mau ngatur image dari awal, gimana?

Tak perlu risau! Docker tahu kok setiap *developer* punya kustomisasi masing-masing. 😁

Docker menyediakan fitur `Dockerfile` yang merupakan satuan file teks yang berisi instruksi untuk membangun *image* Docker secara otomatis. Dengan menggunakan `Dockerfile`, proses pengembangan dapat dilakukan secara otomatis dan lingkungan kontainer dapat direplikasi dengan mudah.

Yuk, kita bermain lagi.

1. Buatlah file bernama `Dockerfile` di sebuah folder yang akan menjadi tempat proyek.

2. Gunakan potongan kode berikut untuk mengisi file tersebut.

    ```dockerfile
    FROM python:3.9
    WORKDIR /app
    COPY . .
    RUN pip install -r requirements.txt
    CMD ["python", "app.py"]
    ```

3. Jalankan perintah `docker build` untuk membuat *image* Docker berdasarkan konfigurasi `Dockerfile` yang dibuat.

### Eh bentar, isi filenya ngapain emang?

Jadi, `Dockerfile` di atas akan mengambil *image* `python:3.9` sebagai *base image*. Setelah itu, direktori `/app` diatur sebagai *working directory* dari kontainer. Lalu, semua file proyek disalin ke dalam kontainer. Perintah `pip install -r requirements.txt` kemudian dijalankan untuk menginstal dependensi aplikasi. Di akhir file, perintah `python app.py` dijalankan saat kontainer dijalankan sebagai sebuah perintah (*command*).

Kamu dapat mempelajari `Dockerfile` lebih lanjut melalui [Docker Docs](https://docs.docker.com/engine/reference/builder/).

## Canggih banget!

Tunggu! Masih ada fitur yang lebih canggih daripada `Dockerfile`; sambutlah [Docker Compose](https://docs.docker.com/compose/).

Compose adalah sebuah alat untuk mendefinisikan dan menjalankan aplikasi Docker secara multi-kontainer. Dengan Compose, kamu menggunakan file YAML untuk mengatur layanan aplikasi kamu; dengan satu perintah, kamu dapat membuat dan menjalankan semua layanan dari konfigurasi yang kamu buat.

Compose dapat mengelola siklus hidup aplikasimu. Compose dapat:

- Memulai, menghentikan, dan membangun ulang layanan
- Melihat status layanan yang sedang berjalan
- Mencetak log dari layanan yang sedang berjalan
- Menjalankan perintah sekali jalan pada suatu layanan

Fitur utama Compose yang membuatnya efektif adalah:

- Memiliki beberapa lingkungan yang terisolasi pada satu induk
- Mempertahankan data volume saat kontainer dibuat
- Hanya membuat ulang kontainer yang telah berubah
- Mendukung variabel dan memindahkan komposisi antarlingkungan

Yak, mari kita bermain lagi.

1. Buatlah file bernama `docker-compose.yml` di sebuah folder yang sama dengan folder `Dockerfile` yang sudah dibuat sebelumnya.

2. Gunakan potongan kode berikut untuk mengisi file tersebut.

    ```yaml
    version: '3'
    services:
    web:
        build:
        context: .
        dockerfile: Dockerfile
        ports:
        - 8080:80
    ```

3. Jalankan perintah `docker-compose up` untuk menjalankan semua layanan yang didefinisikan dalam file Docker Compose.

File di atas mendefinisikan sebuah layanan bernama `web` yang akan dibangun menggunakan `Dockerfile` yang ada di direktori saat ini (`context: .`) dan akan menghubungkan *port* `8080` dari mesin *host* ke *port* `80` pada kontainer.

Kamu dapat mempelajari `Docker Compose` lebih lanjut melalui [Docker Docs](https://docs.docker.com/compose/compose-file/).

## Kira-kira Docker ini sudah terintegrasi dengan apa saja?

Wah, banyak! Sudah banyak IDE dan layanan *hosting* yang mendukung kontainer Docker, seperti Visual Studio Code (IDE), IntelliJ IDEA (IDE), DigitalOcean (*hosting*), Hostinger (*hosting*), dan lain-lain.

## Kira-kira ada nggak strategi deployment Docker?

Lingkungan *staging* dan *production* memainkan peran penting dalam siklus pengembangan perangkat lunak. Docker dapat membantu kamu dalam memindahkan aplikasi dari lingkungan pengembangan ke lingkungan *staging* dan *production*.

Untuk melakukan migrasi, kamu  dapat menggunakan langkah-langkah berikut:

1. Buat file Docker Compose khusus untuk lingkungan *staging* atau *production* dengan konfigurasi yang sesuai.
2. Perbarui file Docker Compose yang ada dengan menggunakan file yang baru dibuat untuk lingkungan *staging* atau *production*.
3. Gunakan perintah `docker-compose up` untuk menjalankan aplikasi di lingkungan *staging* atau *production*.
4. Pastikan untuk melakukan uji coba dan verifikasi aplikasi di lingkungan *staging* sebelum memindahkannya ke lingkungan *production*. Kamu juga dapat menggunakan alat orkestrasi seperti Docker Swarm atau Kubernetes untuk mengelola lingkungan *production* dengan lebih canggih.

## Kalau keamanan, kira-kira best practice-nya gimana?

Berikut adalah beberapa tips dan *best practice* untuk menjaga kontainer aplikasimu tetap aman.

1. Menggunakan *base image* yang terpercaya dan terbaru untuk membangun kontainer.
2. Memperbarui secara rutin kontainer dan *image* dengan versi yang terbaru yang mengandung tambalan keamanan (*security patch*).
3. Mengisolasi kontainer dengan menggunakan fitur seperti `namespaces` dan `cgroups`.
4. Menerapkan prinsip kebutuhan terkecil (*principle of least privilege*) dengan memberikan hak akses yang sesuai ke dalam kontainer.
5. Memantau dan menganalisis log kontainer untuk mendeteksi aktivitas yang mencurigakan.

Selain itu, terdapat alat keamanan tambahan yang dapat digunakan untuk memastikan terjaminnya keamanan pada kontainer, seperti Docker Security Scanning dan Docker Bench Security.

---

Selamat! Kamu telah menjelajahi panduan ringkas menggunakan kontainer berbasis Docker dalam pengembangan perangkat lunak. Sekarang kamu telah memiliki dasar yang kuat untuk mengoptimalkan efisiensi dan portabilitas dalam pengembangan perangkat lunak dengan memahami kontainer Docker hingga *best practice* dalam keamanan kontainer.

Teruslah menggali lebih dalam dan terapkan pengetahuan ini ke dalam proyek kamu. Docker adalah alat yang kuat dan fleksibel yang dapat membantumu dalam mencapai tujuan pengembangan perangkat lunak yang lebih efisien. Selamat berlayar menuju masa depan yang lebih cerah dalam dunia pengembangan perangkat lunak, teman-teman!
