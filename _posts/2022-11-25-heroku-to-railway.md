---
layout: post
title: Pindah dari Heroku ke Railway
categories: [PBP, Heroku, Railway, Django]
---

### bentar, masih cecoret; nanti dirapihin.

<https://railway.app/heroku>

akses database credentials heroku buat dump database terus:

```bash
pg_dump -U <USERNAME> -h <HEROKU_DATABASE_URL> -p <HEROKU_PORT> -W -F t <DATABASE_NAME> > heroku_dump
```

terus buat app baru di railway, kasih akses ke repo, import venv dari heroku (delete yang database utl), terus ubah `settings.py`, ubah details url-nya, buat service postgres, baru import:

```bash
pg_restore --no-privileges --no-owner -U postgres -h <RAILWAY_DATABASE_URL> -p <RAILWAY_PORT> -W -F t -d railway heroku_dump
```

udah deh harusnya kelar, paling restart app atau redeploy.

oh iya, ubah url app biar lebih mudah diakses.

### Cons

Sadly capped to 500 hours of running time per month; jadinya cuma bisa up till 20 days-ish.

## Referensi

- [Migrating From Heroku To Railway](https://blog.railway.app/p/railway-heroku-rails)
- [How to Backup and Restore Your Postgres Database](https://blog.railway.app/p/postgre-backup)
- [How can I download db from heroku?](https://stackoverflow.com/questions/17022571/how-can-i-download-db-from-heroku)
- [pg_restore error: role XXX does not exist](https://stackoverflow.com/questions/37271402/pg-restore-error-role-xxx-does-not-exist)