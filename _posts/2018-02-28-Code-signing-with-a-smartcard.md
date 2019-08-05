---
layout: post
title: "Code signing with a smart card"
date: 2018-02-28 00:00:50 +0200
categories: kali
---

## Install the needed software

```sh
YubiKey-PIV-Tool
YubiKey-PIV-Manager
OpenSC
```

## Import the cert on the Card

Read the public key from the slot 9c :

```sh
pkcs15-tool --read-public-key 02
```

## Signing with the YubiKey

Gen a sha256 hash of the document to sign :

```sh
openssl dgst -sha256 -binary plaintext.txt > plaintext.txt.sha256
```

Sign the sha256 hash of the document using the slot 9c :

```sh
pkcs15-crypt -s -i plaintext.txt.sha256 -o signed.output -f openssl --sha-256 --pkcs1 -k 02
```

## Verifying the Signature

Use the public key to verify the signature :

```sh
openssl dgst -sha256 -verify mykey.pub -signature signed.output plaintext.txt
```
