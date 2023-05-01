---
layout: post
title: Bahas Hosting (Lagi)
categories: [PBP, Django, Hosting]
---

> Will be updated.

1. [DOM Cloud Hosting]

    [DOM Cloud Hosting] merupakan PaaS yang dibuat oleh [Wildan Mubarok](https://wellosoft.net/). Beliau sendiri membuat layanan [DOM Cloud Hosting] karena beliau juga frustasi dengan terbatasnya layanan *hosting* gratis yang dapat digunakan untuk tugas perkuliahan.

    > We want students, teachers, developers with their hobby time make use of our platform for a better experience with putting things online. Personally, the reason I created this because I once struggled to find a host service that's good enough for a university project.

    Sumber: [Our Philosophy - DOM Cloud](https://domcloud.co/docs/intro/philosophy)

    Secara garis besar, layanan gratis yang diberikan oleh [DOM Cloud Hosting] sendiri cukup menggiurkan; kapasitas sebesar 1.5 GB untuk 3 situs web, domain `*.domcloud.io` gratis, dan sertifikat SSL gratis dengan layanan [Let's Encrypt](https://letsencrypt.org/).

    ![Contoh Dashboard](https://i.ibb.co/TwbSTwD/Screenshot-2023-05-02-06-13-05.jpg)

    Berikut adalah contoh konfigurasi YAML untuk Django.

    - Deploy

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

    - Webhook

      Pastikan kamu telah mengatur repositori GitHub yang ingin kamu pakai.

      ```yaml
      commands:
        # Use stash to avoid unstaged changes problem
        - git stash
        - git pull
        - git stash pop
      ```

2. [Adaptable]

    ![Contoh Dashboard](https://i.ibb.co/6RnKVhP/Screenshot-2023-05-02-00-07-01.jpg)

[DOM Cloud Hosting]: https://domcloud.co/
[Adaptable]: https://adaptable.io/
