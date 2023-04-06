---
layout: post
title: Pengembangan Berbasis Tes (PBT)
categories: [Proyek Perangkat Lunak, Software Engineering, Kuliah]
---

> Still in construction, sorry for the inconveniences.

Mungkin konsep ini sudah pernah didengar, namun dalam bahasa lain. Yak, pengembangan berbasis tes adalah *test-driven development*; biasanya disingkat dengan istilah TDD (tapi bukan *T-shirt driven development* 🤭)

Konsep ini sebenarnya cukup kontroversial di dunia pengembangan aplikasi; beberapa *programmer* beranggapan bahwa konsep atau metode ini membutuhkan waktu yang sangat banyak, sehingga proses pengembangan aplikasi menjadi cukup lama dan melelahkan. Namun, manfaat yang diperoleh dari konsep ini tidaklah sedikit.

## Apa sih maksud dari PBT?

Sesuai namanya, pengembangan berbasis tes merupakan konsep pengembangan aplikasi yang dilakukan dengan basis tes. Hal ini berkebalikan dengan metode pengembangan aplikasi pada umumnya. Pertama-tama, kasus uji dibuat terlebih dahulu sebagai pondasi dari pengembangan aplikasi. Lalu, aplikasi dikembangan dengan basis memenuhi kasus uji yang sudah dibuat sebelumnya. Pengembang dapat mengembangkan fungsi lainnya setelah kasus uji yang dibuat sebelumnya terpenuhi.

Berikut adalah siklus pengembangan berbasis tes secara sederhana.

![Gambar Siklus PBT](https://miro.medium.com/v2/resize:fit:475/1*Mjb3IFooRmFumA2IgNEWbw.png)

Pada pengembangan berbasis tes, terdapat tiga fase yang umumnya diketahui; *red*, *green*, dan *refactor*. Secara sekilas, makna dari setiap fase dapat ditebak. Fase *red* berarti fase pembuatan tes sebagai pondasi pengembangan. Warna merah sendiri mengindikasikan status tes yang belum terpenuhi oleh aplikasi, karena tentunya tes baru saja dibuat sehingga belum ada fungsi aplikasi yang memenuhi tes tersebut. Fase *green* berarti fase pembuatan fungsi aplikasi yang memenuhi tes yang telah dibuat sebelumnya. Warna hijau mengindikasikan status tes yang telah terpenuhi oleh fungsi aplikasi yang telah dikembangkan pada fase ini. Fase *refactor* berarti fase improvisasi kode fungsi yang telah dibuat sebelumnya dengan menerapkan prinsip *refactoring*, sehingga prinsip *clean code* dapat terpenuhi.

![Gambar Fase PBT](https://miro.medium.com/v2/resize:fit:700/1*tZSwCigaTaJdovyWlp5uBQ.jpeg)

## Daftar Pustaka

- [Test Driven Development: Arti, Manfaat, dan Cara Melakukannya](https://glints.com/id/lowongan/test-driven-development/)
- [Mengenal Lebih Dalam Test Driven Development (TDD): Pengertian, Jenis Testing, dan Kelebihan TDD](https://www.binaracademy.com/blog/test-driven-development-tdd-adalah)