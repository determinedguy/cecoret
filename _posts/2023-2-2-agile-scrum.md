---
layout: post
title: Agile, Scrum, dan Lainnya
categories: [Proyek Perangkat Lunak, Software Engineering, Kuliah]
---

> Note: Still under construction.

## Agile? Scrum? Apaan tuh?

Ungkapan itu merupakan ungkapan pertama saya saat mendengar terminologi asing tersebut. Istilah ini sangat sering terdengar di dunia pengembangan perangkat lunak pada dunia kerja. Pada tulisan ini, saya akan mengenalkan maksud dari istilah-istilah tersebut (yang kedengarannya sangat *geeky*, hehe).

### Metode Agile

Agile merupakan metodologi pengembangan perangkat lunak yang didasari oleh prinsip pengembangan yang memerlukan adaptasi yang cepat serta prinsip ekonomi yang mengurangi biaya proyek dan meningkatkan nilai jual bisnis di waktu yang sama. Fokus dari Agile adalah terciptanya perangkat lunak yang secara konsisten berkualitas tinggi secara konsisten.

Bisa dikatakan bahwa Agile merupakan metode pengembangan yang cocok untuk pengembangan perangkat lunak yang sering memiliki perubahan yang tak terduga, karena naturalnya Agile bersifat fleksibel dan adaptif terhadap perubahan yang terjadi pada masa pengembangan.

Metode Agile memiliki sebuah manifesto yang terdiri dari empat hal. Manifesto ini mendefinisikan hal-hal utama yang diperhatikan pada Agile.

1. **Individu dan interaksi** lebih dari proses dan sarana perangkat lunak

    Hal ini berarti stabilitas interaksi antar individu yang terlibat pada proyek lebih utama dibandingkan proses dan alat bantu perangkat lunak yang dipakai.

2. **Perangkat lunak yang bekerja** lebih dari dokumentasi yang menyeluruh

    Hal ini berarti perangkat lunak yang bekerja dengan baik lebih baik daripada dokumentasi yang komprehensif.

    > Just like people say; if it works, it works!

    Namun menurutku, dokumentasi tetap perlu, sih.

3. **Kolaborasi dengan klien** lebih dari negosiasi kontrak

    Hal ini berarti kolaborasi yang dilakukan dengan klien secara konsisten lebih baik daripada menyesuaikan kontrak secara terus-menerus (*sampai tidak ada kontrak finalnya*).

4. **Tanggap terhadap perubahan** lebih dari mengikuti rencana

    Hal ini berarti perubahan di tengah proyek tidak apa-apa daripada mengikuti rencana awal secara kaku.

Kalau kalian ingin mengecek Agile Manifesto pada situs web asalnya, kalian dapat mengunjungi [agilemanifesto.org](https://agilemanifesto.org/iso/id/manifesto.html).

Secara konsep, terdapat banyak macam penerapan dari metode Agile. Beberapa tahapan Agile adalah sebagai berikut.

1. Penemuan

    Sebelum memulai sebuah proyek baru, kita perlu memahami visi atau objektif dari klien atau user yang memiliki kepentingan dan kepemilikan dalam proyek tersebut. Tahap ini dimulai dengan sebuah riset untuk mencapai pengertian akan tujuan yang ingin dicapai oleh klien, tantangan yang ada, iklim bisnis sekarang, serta user. Tahap ini termasuk memastikan adanya pengertian yang sama di antara klien, *Project Manager*, *Designer*, *Developer*, dan *Product Owner*.

2. *Product Backlog*

    Setelah proses penemuan, tim akan mulai bekerja bersama untuk membuat sebuah *Product Backlog* yang berisi daftar fitur yang akan berguna bagi klien dan user. *Product Owner* akan bekerja sama dengan klien untuk memprioritaskan fitur dan menentukan urutan dari bagaimana fitur akan dirancang, dikembangkan, dites, dan diterapkan. Hal ini akan membantu tim untuk tetap fokus dalam memberikan fitur dengan nilai tinggi sebelum bekerja pada tugas yang berprioritas lebih rendah.

3. Iterasi

    Setelah memastikan bahwa tim mengerti visi yang dimiliki oleh klien dan membuat sebuah *product backlog* yang tepat, tim akan mulai menerapkan fitur-fitur yang telah dibuat dalam sebuah pengulangan atau iterasi yang diukur oleh waktu. Iterasi ini sendiri dinamakan **Sprint**. Sprint sendiri berlangsung selama satu sampat empat minggu, tergantung dari besar proyek dan durasi waktu yang ada. Setiap Sprint akan memenuhi objektif atau target yang ada pada *product backlog*.

4. Penerusan Siklus

    Sprint tambahan akan dilakukan sesuai dengan yang dibutuhkan untuk menghasilkan fitur tambahan dan memasukan umpan balik yang didapat dari tinjauan sebelumnya. Setiap Sprint baru harus menghasilkan perkembangan dari hasil Sprint sebelumnya dan juga menghasilkan fitur baru ke dalam sistem.

Agile sendiri hanyalah merupakan metode pengembangan. Untuk mewujudkan tujuan dari Agile, maka kita perlu menerapkan beberapa metode terapan dari Agile. Salah satunya adalah Scrum.

### Scrum

Scrum merupakan metode terapan dari metodologi Agile yang berfungsi untuk untuk mengatur pengelolaan dan pelaksanaan proyek. Scrum sendiri bersifat fleksibel, sehingga metode ini cocok untuk proyek yang bersifat kompleks dan sering mengalami perubahan.

Konsep utama dalam Scrum adalah pengamatan empiris dan *lean thinking*. Pengamatan empiris mengharuskan tim untuk menentukan keputusan berdasarkan data dan *lean thinking* mengharuskan tim untuk fokus ke hal utama terlebih dahulu.

Scrum memiliki tiga pilar utama yang bersifat empiris, yakni transparansi, inspeksi, dan adaptasi.

1. Transparansi

    Transparansi yang dimaksud adalah transparansi informasi dan proses yang dilakukan oleh individu yang bertanggung jawab atas sebuah *backlog* pada proyek.

2. Inspeksi

    Inspeksi yang dimaksud adalah pengecekan validasi atas hasil kerja yang dilakukan oleh individu yang bertanggung jawab atas sebuah *backlog* pada proyek.

3. Adaptasi

    Adaptasi yang dimaksud adalah proses adaptasi yang dilakukan oleh tim apabila terjadi sesuatu yang berbeda dari rencana sebelumnya setelah meninjau dua pilar sebelumnya, sehingga perubahan harus dilakukan agar tim dapat memberikan hasil yang terbaik sesuai dengan *product backlog*.

Berikut adalah ilustrasi pilar Scrum yang dapat menggambarkan maksud dari setiap pilar secara singkat.

![Ilustrasi Pilar Scrum](https://lh4.googleusercontent.com/FSC5tt6MzXd7POxyo6r-ZNkbIzJ61QQHDj_jHzxad6mxQK9MqheOItQRq2HHKG97nZMsF7SW50DSR5M6EAdJuNX1ltYGh6d1tCgQ9IZnQ-Oef-1Vr1_qX8iWJ85PU4TmMCuLJkj3)

Secara ringkas, Scrum terdiri dari empat fase.

1. *Inception* (Sprint 0)

    Pada fase ini, visi proyek diperjelas dengan adanya pembuatan *Product Requirement Document* (PRD). Selain itu, *epic* mulai didefinisikan dan dielaborasikan. *Epic* sendiri merupakan pekerjaan-pekerjaan besar yang dapat dipecah menjadi beberapa bagian yang lebih kecil. *Product backlog* pun mulai disusun dan *user story*-nya didefinisikan dengan kriteria **INVEST** (Independent, Negotiable, Valuable, Estimate-able, Small, Testable).

2. *Sprint Planning*

    Pada fase ini, tim memutuskan *backlog* apa saja yang akan dikerjakan di sebuah sprint. Pertimbangan yang dipakai dapat berupa *value* yang diberikan setelah sprint selesai, jumlah *backlog* yang dapat diselesaikan dalam satu sprint, dan cara penyelesaian *backlog* yang telah dipilih untuk dikerjakan.

3. *Sprint* (*Core*)

    Pada fase ini, setiap implementasi kode dari *user story* yang digunakan harus dimasukkan ke dalam repositori. Selain itu, *Scrum Board* harus diperbarui secara berkala; contohnya apakah *task* yang dikerjakan sudah selesai atau belum.

    *Daily standup meeting* dilakukan minimal dua kali per minggu. Hari untuk *daily standup meeting* ditentukan sejak awal, bersifat *fixed* untuk setiap minggunya, dan berselang minimal dua hari. Pada setiap *daily standup meeting*, sebaiknya sudah ada *merge request* dari setiap individu yang terlibat. *Backlog* diperbarui dan di-*maintain* secara rutin oleh *Product Owner* apabila diperlukan.

4. *Sprint Review* dan *Sprint Retrospective*

    Setelah menyelesaikan Sprint, ada baiknya untuk merefleksikan apa yang telah dilakukan sebelumnya agar Sprint selanjutnya bisa lebih baik. Karena itulah adanya fase ini. 😉

### Kapan sebaiknya Scrum dipakai?

Beruntungnya, [Ralph Stacey](https://en.wikipedia.org/wiki/Ralph_D._Stacey) telah membuat sebuah diagram yang mengilustrasikan penyesuaian kebutuhan proyek dengan realisasi teknologi yang dapat dilakukan.

![Stacey Matrix](https://d1dwq032kyr03c.cloudfront.net/upload/images/20190901/20106486xmqWZDWa46.jpg)

Kalau proyek memiliki *requirements* yang jelas dan teknologinya khalayak terkenal atau simpel, maka sebaiknya tidak usah menggunakan metode-metode *fancy* ini (karena lebih baik tidak menyusahkan diri sendiri, hehe); sebaiknya pakai Waterfall saja.

Kalau proyeknya nggak jelas, teknologinya masih asing, skalanya kompleks (waduh!), mending pakai metode terapan lainnya.

### Emang ada metode terapan Agile selain Scrum?

Ada, dong!

- *Extreme Programming* (XP)

    Metode terapan ini sangat identik dengan *pair programming*; membuat program secara berdampingan agar ada umpan balik secara kontinu. XP berfokus pada komunikasi, kesederhanaan, umpan balik, rasa hormat (*respect*), dan keberanian.

    Kalau kamu tertarik dengan metode XP, kamu dapat membacanya lebih lanjut [disini](https://serupa.id/extreme-programming-xp-definisi-nilai-tahapan/).

- Crystal

    Metode ini jarang didengar, namun tetap menjadi salah satu opsi yang lumayan diketahui oleh perusahaan-perusahaan besar. Tidak seperti metodologi lainnya, metode Crystal Agile memprioritaskan interaksi, orang, keterampilan, bakat, dan komunikasi daripada proses dan alat bantu. Dengan prinsip tersebut, Crystal meningkatkan produktivitas tim dan membuat setiap produk bersifat unik.

    Kalau kamu tertarik dengan metode Crystal, kamu dapat membacanya lebih lanjut [disini](https://monday.com/blog/project-management/agile-crystal/).

- Kanban

    Kalau kalian pernah lihat *Kanban Board*, ya ... memang ini yang dimaksud. 😊

    *Kanban Board* biasanya dibagi menjadi empat bagian; *to-do*, *code*, *testing*, dan *done*. Dengan adanya visualisasi berupa *Kanban Board*, tingkat fleksibilitas pengerjaan proyek dapat lebih terkontrol karena kita dapat mengetahui apakah ada *bottleneck* dan kesalahan yang dapat dengan mudah diubah.

    ![Contoh Kanban Board](https://sis.binus.ac.id/wp-content/uploads/2018/03/yttrytr-640x321.png)

    Kamu dapat membaca informasi mengenai Kanban lebih lanjut [disini](https://sis.binus.ac.id/2018/03/09/knowing-agile-development-methodologies-kanban/).

### Jadi, pilih yang mana dong?

Tinjau dengan skala dan teknologi proyek, lalu sesuaikan dengan Stacey Matrix yang sebelumnya telah dibahas. Tidak semua proyek perlu menggunakan metode *geeky* ini, dan tidak semua proyek dapay diselesaikan dengan metode Scrum karena ... *it's not one-size-fits-all*! Diskusikan juga dengan individu dan tim yang terlibat dalam pengembangan proyek.

Setelah mendapatkan metode yang sesuai dengan keadaan, *don't forget to work responsibly and have fun*! 😉

### Daftar Pustaka

- [Wiki PPL CSUI](https://wiki.ppl.cs.ui.ac.id/doc/panduan-scrum-ZD0IkkG3si)
- [Pengeritan Agile dan Scrum - Hacktiv8 Blog](https://blog.hacktiv8.com/membedah-pengertian-agile-scrum/)
- [Mengenali Konsep Agile, Scrum, dan Sprint a la Perusahaan IT - Binar Academy](https://www.binaracademy.com/blog/mengenali-konsep-agile-scrum-dan-sprint)
- [Apa itu Scrum? - AWS](https://aws.amazon.com/id/what-is/scrum/)
- [The Stacey Matrix - Explained - The Business Professor, LLC](https://thebusinessprofessor.com/management-leadership-organizational-behavior/the-stacey-matrix-explained)
