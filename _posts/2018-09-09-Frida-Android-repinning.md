---
layout: post
title: "Frida android repinning"
date: 2018-09-09 00:00:50 +0200
categories: kali
---

Installation of frida

```sh
pip3 install frida
pip3 install objection
```

Download frida-server (for the target)

```sh
wget https://github.com/frida/frida/releases/download/12.1.2/frida-server-12.1.2-android-arm.xz
xz –decompress frida-server-12.1.2-android-arm.xz
```

Setup frida-server on the phone

```sh
adb push frida-server-12.1.2-android-x86 /data/local/tmp/frida-server
adb shell chmod 777 /data/local/tmp/frida-server
adb shell "su -c '/data/local/tmp/frida-server &'"
```

Connect to frida server

```sh
# New terminal :
frida-ps -U # USB
frida-ps -R 127.0.0.1 # Remote connection (via Wifi)
frida-ps -H 127.0.0.1 # Remote connection
```

To inject script into the app

```sh
frida -U -f mobi.societegenerale.mobile.lappli.hf.sg -l ANYTHING.js –no-pause
```

- `-U` # USB
- `-f [Package name]` # Package name
- `-l` # location of the script
- `--no-pause` # automatically start main thread after startup

See [https://www.frida.re/docs/home/](https://www.frida.re/docs/home/) to learn how to build and inject any script on the apps
or download scripts from [https://github.com/](https://github.com/) or [https://codeshare.frida.re/](https://codeshare.frida.re/)

Inject the Burp certificate to bypass the ssl pinning

```sh
adb push burpca-cert-der.crt /data/local/tmp/cert-der.crt
frida -U -f mobi.societegenerale.mobile.lappli.hf.sg -l frida-android-repinning.js –no-pause
```

or

```sh
frida –codeshare pcipolloni/universal-android-ssl-pinning-bypass-with-frida -f YOUR_BINARY
```
