---
layout: post
title: 'Fix GPG error "NO_PUBKEY"'
date: 2019-06-08 00:00:50 +0200
categories: proxy
---

{% highlight sh %}
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com KEY_ID
{% endhighlight %}

voir :
[https://doc.ubuntu-fr.org/apt-key](https://doc.ubuntu-fr.org/apt-key)
