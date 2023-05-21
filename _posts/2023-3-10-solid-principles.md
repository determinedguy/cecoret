---
layout: post
title: Prinsip SOLID untuk Pemrograman Berbasis Obyek
categories: [Proyek Perangkat Lunak, Software Engineering, Kuliah]
---

## "Kita harus SOLID!"

> Waduh, ampun bang!

Bukan, bukan; kita lagi nggak di ospek, kok.

Tidak sedikit dari kita yang telah mengenali konsep pemrograman berbasis obyek (*object-oriented programming*), namun tidak sedikit pula yang tidak pernah mendengar sebuah set prinsip pemrograman yang berkaitan dengan konsep pemrograman berbasis obyek dan seringkali disebut dengan akronim SOLID.

![SOLID](https://www.thoughtworks.com/content/dam/thoughtworks/images/photography/inline-image/insights/blog/agile-engineering-practices/blg_inline_solid_principles.png)

## Gimana ceritanya kok bisa ada SOLID?

Prinsip SOLID dikenalkan oleh Robert Martin (alias *Uncle Bob*) pada tahun 2000 di salah satu *paper*-nya ([Design Principles and Design Patterns](web.archive.org/web/20191116231621/fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf)). Awalnya prinsip SOLID hanya berbentuk sebuah himpunan konsep yang tidak memiliki akronim tersendiri. Michael Feathers lah yang mengenalkan akronim SOLID pada sekitar tahun 2004 dan akhirnya akronim tersebut diadopsi secara khalayak umum.

Tujuan dari prinsip SOLID adalah untuk mendorong pembuatan perangkat lunak yang lebih mudah dipelihara, mudah dipahami, dan fleksibel. Dengan demikian, kompleksitas aplikasi dapat dikurangi seiring dengan berkembangnya ukuran atau skala aplikasi tersebut. Jadinya nggak sakit kepala, deh.

## Apa tuh maksudnya SOLID?

Prinsip SOLID sendiri terdiri dari lima prinsip, sesuai dengan singkatannya.

![SOLID Principles](https://devopedia.org/images/article/177/8101.1558682601.png)

1. **S**ingle Responsibility

    Prinsip ini menyatakan bahwa sebuah kelas harus memiliki satu dan **hanya** satu alasan untuk berubah, sehingga berarti bahwa sebuah kelas **hanya boleh memiliki satu pekerjaan**.

    Bagaimana prinsip ini (yang biasa disingkat menjadi SRP) dapat menolong kita untuk membuat perangkat lunak yang kokoh? Mari kita lihat tiga kasus berikut.

    1. Pengetesan

        Dengan prinsip SRP, kasus uji yang perlu dibuat untuk sebuah kelas menjadi lebih sedikt. Hal ini dikarenakan tanggung jawab kelas yang diuji dipastikan hanya berupa satu pekerjaan.

    2. *Lower coupling*

        Dependensi antar kelas tentunya akan berkurang karena sebuah kelas memiliki fungsionalitas yang lebih sedikit.

    3. Struktur Organisasi

        Kelas yang lebih kecil dan teratur tentunya lebih mudah dicari daripada kelas monolitik.

    Contoh kasus untuk prinsip ini adalah sebagai berikut.

    Misalkan ada sebuah kelas yang mengandung informasi terkait profil seorang mahasiswa. Pada kelas tersebut, kita menyimpan informasi berupa nama, nomor identitas, jurusan, dan status keaktifan mahasiswa.

    ```java
    public class Profile {

        private String name;
        private long idNumber;
        private String major;
        private boolean isActive;

        //constructor, getter dan setter
    }
    ```

    Mari kita coba tambahkan fungsi tambahan yang berhubungan langsung dengan atribut kelas `Profile`.

    ```java
    public class Profile {

        private String name;
        private long idNumber;
        private String major;
        private boolean isActive;

        //constructor, getter dan setter

        // fungsi yang berhubungan langsung dengan atribut profil
        public String replaceMajor(String oldMajor, String newMajor){
            return major.replaceAll(oldMajor, newMajor);
        }
    }
    ```

    Wah! Sepertinya kelas `Profile` sekarang bersih. Namun, bagaimana jika kita ingin membuat fungsi *logging* untuk mencetak informasi profil? Apakah kita akan membuatnya di dalam kelas `Profile`?

    Tentu tidak, karena hal ini melanggar SRP. 😉

    Oleh karena itu, kita perlu membuat kelas terpisah untuk membuat fungsi *logging* kelas `Profile`.

    ```java
    public class ProfileLogger {

        // fungsi cetak profil 
        void printProfileInfo(String text){
            // kode cetak profil
        }

        void printProfileInfoToWebsite(String text){
            // kode cetak profil ke situs web
        }
    }
    ```

    Dengan demikian, setiap kelas menerapkan SRP dengan baik dan benar.

2. **O**pen-Closed

    Prinsip ini menyatakan bahwa obyek atau entitas harus **terbuka untuk ekstensi**, namun **tertutup untuk modifikasi**. Dengan menerapkan prinsip ini, kita mencegah adanya modifikasi kode yang sudah ada dan potensi bug baru dalam aplikasi yang sejauh ini berjalan dengan baik.

    Tentunya, memperbaiki bug dalam kode yang sudah ada menjadi kondisi pengecualian pada prinsip ini.

    Sebagai contoh, kita membuat aplikasi yang memiliki sebuah *class* Piano yang lengkap (bahkan kekuatan pedalnya diatur di *class*!).

    ```java
    public class Piano {
        private String brand;
        private String model;
        private int keys;
        private int pedal;

        //Konstruktor, getter, dan setter
    }
    ```

    Tak lama, aplikasi diluncurkan dan semua pengguna menyukainya. Setelah beberapa bulan, sebuah ide muncul sebagai bentuk improvisasi; "kayaknya enak nih kalau pianonya punya warna kustom!"

    Pada saat ini, mungkin kita tergoda untuk membuka *class* Piano dan menambahkan warna kustom. Tapi tunggu; tentunya hal ini menyalahi prinsip *Open-Closed*! Siapa tahu akan ada kesalahan yang mungkin muncul dalam aplikasi kita setelah kita melakukan hal tersebut.

    Sebagai gantinya, mari kita tetap mematuhi prinsip *open-closed* dan hanya memperluas *class* Piano yang telah dibuat sebelumnya.

    ```java
    public class PianoWithCustomColor extends Piano {
        private String customColor;

        //Konstruktor, getter, dan setter
    }
    ```

    Dengan memperluas *class* Piano melalui ekstensi, kita dapat memastikan bahwa kode aplikasi yang sudah ada tidak akan terpengaruh oleh kode yang baru saja dibuat.

    > Penerapan *Open-Closed* berhasil!

3. **L**iskov Substitution

    > Misalkan q(x) adalah properti yang dapat dibuktikan tentang objek x bertipe T, maka q(y) harus dapat dibuktikan untuk objek y bertipe S di mana S adalah subtipe dari T.

    Hayo loh, bingung nggak tuh? Memang sih, prinsip ini paling kompleks dibandingkan prinsip-prinsip lainnya pada prinsip SOLID ....

    Sederhananya sih, jika kelas A adalah **subjenis** dari kelas B, maka kita **harus dapat mengganti** B dengan A **tanpa mengganggu perilaku program**.

    Langsung lihat contoh aja, deh!

    Misalkan kita memiliki *interface* Bus dengan metode-metode yang harus dipenuhi oleh sebuah bus: menyalakan mesin dan akselerasi.

    ```java
    public interface Bus {
        void turnOnEngine();
        void accelerate();
    }
    ```

    Mari implementasikan *interface* ini dan berikan beberapa kode untuk metode-metode tersebut.

    ```java
    public class Bikun implements Bus {
        private Engine engine;

        //Konstruktor, getter, dan setter

        public void turnOnEngine() {
            engine.on();
        }

        public void accelerate() {
            engine.powerOn(1000);
        }
    }
    ```

    Seperti yang dijelaskan oleh kode kita, kita memiliki sebuah mesin yang dapat kita hidupkan dan kita dapat meningkatkan kekuatannya.

    Tapi tunggu, sekarang kan eranya bus listrik!

    ```java
    public class BikunListrik implements Bus {
        public void turnOnEngine() {
            throw new AssertionError("Saya tidak memiliki mesin!");
        }

        public void accelerate() {
            //akselerasi ini luar biasa!
        }
    }
    ```

    Dengan memasukkan bus tanpa mesin ke dalam program, kita mengubah perilaku program kita secara mendasar. Hal ini merupakan **pelanggaran nyata** terhadap prinsip *Liskov substitution* dan sedikit lebih sulit untuk diperbaiki daripada dua prinsip sebelumnya.

    Berikut adalah contoh penerapan prinsip *Liskov substitution*  yang benar untuk kasus bus.

    ```java
    public interface Vehicle {
        void startEngine();
        void accelerate();
    }

    public class Car implements Vehicle {
        private Engine engine;
        
        public void startEngine() {
            engine.start();
        }
        
        public void accelerate() {
            engine.increasePower(100);
        }
    }

    public class Bus implements Vehicle {
        private Engine engine;
        private boolean doorsOpen;
        
        public void startEngine() {
            engine.start();
        }
        
        public void accelerate() {
            engine.increasePower(50);
        }
        
        public void openDoors() {
            // Membuka pintu bus
            doorsOpen = true;
        }
        
        public void closeDoors() {
            // Menutup pintu bus
            doorsOpen = false;
        }
    }
    ```

    Dalam contoh ini, *interface* Vehicle memiliki metode `startEngine()` dan `accelerate()`. Kelas Car dan Bus mengimplementasikan *interface* ini.

    Kelas Car merepresentasikan sebuah mobil dengan mesin dan memiliki fungsionalitas untuk menyalakan mesin dan mempercepat.

    Kelas Bus juga merepresentasikan sebuah kendaraan dengan mesin, tetapi memiliki fitur tambahan yaitu membuka dan menutup pintu bus. Meskipun kelas Bus memiliki perilaku yang berbeda saat mempercepat (menggunakan peningkatan kekuatan yang lebih rendah), ia tetap mematuhi prinsip Liskov karena ia dapat digunakan sebagai pengganti dari kelas Vehicle tanpa mengganggu perilaku program.

    Dengan adanya prinsip Liskov, kita dapat menggunakan objek Bus di tempat objek Car tanpa menyebabkan masalah atau konflik pada program yang mengandalkan antarmuka Vehicle.

4. **I**nterface Segregation

    Prinsip ini menyatakan bahwa klien **tidak boleh dipaksa** untuk **mengimplementasikan antarmuka yang tidak digunakannya** atau **bergantung pada metode yang tidak mereka gunakan**.

5. **D**ependency Inversion

    Prinsip ini menyatakan bahwa entitas harus bergantung pada abstraksi, bukan pada konkresi. Dengan kata lain, modul tingkat tinggi tidak boleh bergantung pada modul tingkat rendah, tetapi mereka harus bergantung pada abstraksi.

## Kenapa harus SOLID?

Inti dari prinsip SOLID adalah untuk mengurangi dependensi sehingga kita dapat mengubah suatu bagian dari perangkat lunak sewaktu-waktu tanpa memengaruhi bagian lainnya. Dengan demikian, para pengembang perangkat lunak dapat memperbesar skala perangkat lunak tanpa harus pusing pala Barbie. 😆

## Daftar Pustaka

- [SOLID: The First 5 Principles of Object Oriented Design](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)
- [The SOLID Principles of Object-Oriented Programming Explained in Plain English](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)
- [A Solid Guide to SOLID Principles](https://www.baeldung.com/solid-principles)
- [SOLID Design Principles](https://devopedia.org/solid-design-principles)
