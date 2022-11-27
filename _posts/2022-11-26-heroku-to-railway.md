---
layout: post
title: Pindah dari Heroku ke Railway
categories: [PBP, Heroku, Railway, Django]
---

## Bye bye, Heroku!

Seperti yang telah kita ketahui bersama, *free tier* dari Heroku Dynos, Postgres dan Data for Redis sudah tidak ada lagi setelah 28 November 2022. Tentunya hal ini mengecewakan kita semua sebagai pemakai Heroku yang setia untuk segala tugas kuliah. 🥹

Sudah dilakukan pencarian, penelitian, dan percobaan selama beberapa bulan belakangan oleh tim asisten dosen Pemrograman Berbasis Platform dan ... susah sekali gais ternyata nyari PaaS yang nggak *self-host* dan bisa menyediakan kemampuan yang sama seperti *free tier* Heroku. 💔

Salah satu solusi yang "mendingan" adalah [Railway](https://railway.app/). Kenapa "mendingan" (pakai tanda kutip)? Berikut adalah kelebihan dan kekurangan dari Railway.

- Plus
    - Nggak butuh kartu kredit 🤩
    - Mendukung migrasi dari Heroku secara *out-of-the-box* 😍
    - Dukungan basis data (termasuk PostgreSQL)
    - Menyediakan *hosting* secara gratis (tentunya dengan domain khusus)
    - Aplikasi nyala terus (nggak kayak Heroku yang **sengaja** mematikan aplikasi jika tidak dipakai dalam kurun waktu tertentu) 🥳
- Minus
    - Per bulan cuma dikasih jatah USD 5 dan 500 jam *running time*; aplikasi akan dimatikan *deployment*-nya saat salah satu dari keduanya habis duluan.

        Kalau diestimasi, aplikasi bisa nyala secara terus-menerus selama 20 harian per bulan.

        Kalau udah mati, gimana? Harus *restart* ulang aplikasi secara manual, gais.

Yakin mau lanjut migrasi ke rel kereta api? Oke lanjut~

## Konfigurasi Proyek

**Diasumsikan proyek Django kamu bernama** `project_django`.

1. Buka file `Procfile` dan ubah isi file menjadi seperti berikut.

    ```sh
    web: python manage.py migrate && gunicorn project_django.wsgi
    ```

2. Jika kamu menggunakan templat dari "zaman baheula" (<https://github.com/laymonage/django-template-heroku>), buka file `settings.py` yang ada pada folder `project_django/` perhatikan bagian berikut.

    ```python
    ALLOWED_HOSTS = [f'{HEROKU_APP_NAME}.herokuapp.com']
    ```

    Ubahlah menjadi seperti berikut ini.

    ```python
    ALLOWED_HOSTS = [f'{HEROKU_APP_NAME}.up.railway.app']
    ```

    Jika kamu menggunakan templat dari PBP Ganjil 2022/2023 (<https://github.com/pbp-fasilkom-ui/django-pbp-template>), kamu tidak perlu melakukan langkah ini.

3. Hapus file workflow yang ada pada folder `.github/workflows/` (atau kalau mau, hapus saja foldernya sekalian).

4. Jangan lupa untuk `add`-`commit`-`push` ke GitHub.

## Registrasi Akun dan Impor Repositori

1. Buka situs web [Railway](https://railway.app/heroku) dan klik tombol `New Project`.

2. Klik pilihan `Deploy from GitHub repo`.

3. Klik tombol `Login With GitHub` dan masuklah ke dalam akun GitHub kamu.

4. Kamu akan kembali ke halaman pembuatan proyek baru. Klik pilihan `Deploy from GitHub repo` dan klik `Configure GitHub App`.

5. Pilihlah organisasi kelompok kamu dan klik `Install & Authorize`.

6. Kamu akan kembali ke halaman pembuatan proyek baru. Klik pilihan `Deploy from GitHub repo` dan pilih repositori proyek tengah semester kelompok kamu.

7. Klik `Deploy Now`.

## Impor Variabel Heroku

**Jika kamu tidak memiliki *environment variables* pada proyek Heroku kamu, kamu dapat melewati langkah ini.**

1. Buka servis web, klik `Variables`, tekan Control + K atau Command + K, dan pilih menu `Import Variables From Heroku`.

2. Klik `Connect` dan sesuaikan pengaturan sesuai akun dan proyek yang telah dibuat sebelumnya.

3. Kamu akan kembali ke halaman utama. Tekan Control + K atau Command + K dan pilih menu `Import Variables From Heroku`.

4. Pilih nama proyek tengah semester kamu yang kamu pakai di Heroku.

5. Hapus variabel `DATABASE_URL` karena kita akan memakai servis PostgreSQL dari Railway.

## Ekspor Basis Data dari Heroku

**Pastikan kamu telah menginstal PostgreSQL di komputer lokalmu.**

1. Buka situs web [Heroku](https://dashboard.heroku.com/apps) dan buka proyek tengah semester kamu.

2. Buka menu `Resources` dan klik `Heroku Postgres`.

3. Buka menu `Settings` dan klik `View Credentials…`. Simpanlah informasi mengenai basis data Heroku di suatu tempat (contohnya Notepad).

4. Buka Terminal atau Command Prompt dan jalankan perintah berikut.

    ```bash
    pg_dump -U <USERNAME> -h <HEROKU_DATABASE_HOST> -p <HEROKU_PORT> -W -F t <DATABASE_NAME> > heroku_dump
    ```

## Membuat dan Mengimpor Basis Data di Railway

**Pastikan kamu telah menginstal PostgreSQL di komputer lokalmu.**

1. Bukalah halaman utama proyek di Railway dan tekan Control + K atau Command + K.

2. Pilih `New Service -> Database -> Add PostgreSQL`.

3. Buka servis PostgreSQL dan buka menu `Variables`. Simpanlah informasi mengenai basis data Railway di suatu tempat (contohnya Notepad).

4. Buka Terminal atau Command Prompt dan jalankan perintah berikut.

    ```bash
    pg_restore --no-privileges --no-owner -U postgres -h <RAILWAY_DATABASE_URL> -p <RAILWAY_PORT> -W -F t -d railway heroku_dump
    ```

## Konfigurasi Tambahan: URL

1. Buka servis `web` dan buka menu `Settings`.

2. Perhatikan bagian `Domains` dan ubahlah URL sesuai dengan URL sebelumnya yang dipakai di Heroku.

### Dah, kelar.

## Trivia

> Padahal aslinya hari ini (26 November 2022) mau nginep sama Ayah (kebetulan lagi di Jakarta),
> tapi kerjaan ini belum kelar 😭 yaudahlahya 😔

## Referensi

- [Migrating From Heroku To Railway](https://blog.railway.app/p/railway-heroku-rails)
- [How to Backup and Restore Your Postgres Database](https://blog.railway.app/p/postgre-backup)
- [How can I download db from heroku?](https://stackoverflow.com/questions/17022571/how-can-i-download-db-from-heroku)
- [pg_restore error: role XXX does not exist](https://stackoverflow.com/questions/37271402/pg-restore-error-role-xxx-does-not-exist)