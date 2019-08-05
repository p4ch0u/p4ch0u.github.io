---
layout: post
title:  "Setting Kali linux docker image"
date:   2019-04-09 00:00:50 +0200
categories: kali
---
See the official guide to get the kali docker image at [Official Kali Linux Docker Images Released][kali-docker]

{% highlight sh %}
$ docker pull kalilinux/kali-linux-docker
$ docker run -t -i kalilinux/kali-linux-docker /bin/bash
root@0744557eb512:/# apt-get update && apt-get install metasploit-framework
{% endhighlight %}

To build Your Own Kali Linux Docker Image (Require to be on a linux env)

#TODO

[kali-docker]: https://www.kali.org/news/official-kali-linux-docker-images/

