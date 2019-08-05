---
layout: post
title: "Creer un certificat x509"
date: 2016-05-31 00:00:50 +0200
categories: proxy
---

La manière la plus simple pour créer un certificat x509 :

```sh
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout test.pem -out test.pem
```

ou

```sh
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout test.key -out test.cert
```

See [https://www.openssl.org/docs/man1.0.2/apps/http://www.google.com/search?q=openssl+self-signed+certificat](https://www.openssl.org/docs/man1.0.2/apps/http://www.google.com/search?q=openssl+self-signed+certificat)
