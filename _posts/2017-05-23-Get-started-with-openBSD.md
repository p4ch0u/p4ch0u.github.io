---
layout: post
title: "Getting started with OpenBSD"
date: 2017-05-23 00:00:50 +0200
categories: OpenBSD
---

# Install a program on OpenBSD

Use `pkg_add`

The dirty way :

```sh
pkg_add http://ftp.fr.openbsd.org/pub/OpenBSD/$(uname -r)/packages/\$(arch -s)/firefox
```

The clean way :

```sh
echo "export PKG_PATH=http://ftp.fr.openbsd.org/pub/OpenBSD/$(uname -r)/packages/\$(arch -s)/" >> ~/.profile
```

or

```sh
echo "installpath = http://ftp.fr.openbsd.org/pub/OpenBSD/%v/packages/%a" >> /etc/pkg.conf
```

then

```sh
pkg_add firefox
```

Find a packgage :

```sh
pkg_info -Q pkgName
```

List installed pkg :

```sh
pkg_info
```

List pkg contents:

```sh
pkg_info -L pkgName
```

Thanks to [yeuxdelibad](https://yeuxdelibad.net)
