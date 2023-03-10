---
layout: post
title: Prinsip SOLID untuk Pemrograman Berbasis Obyek
categories: [Proyek Perangkat Lunak, Software Engineering, Kuliah]
---

> Still in construction, sorry for the inconveniences.

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

2. **O**pen-Closed

    Prinsip ini menyatakan bahwa obyek atau entitas harus **terbuka untuk ekstensi**, namun **tertutup untuk modifikasi**.

3. **L**iskov Substitution

    > Misalkan q(x) adalah properti yang dapat dibuktikan tentang objek x bertipe T, maka q(y) harus dapat dibuktikan untuk objek y bertipe S di mana S adalah subtipe dari T.

    Hayo loh, bingung nggak tuh?

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
