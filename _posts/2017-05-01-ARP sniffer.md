---
layout: post
title: "ARP sniffer"
date: 2017-05-01 00:00:50 +0200
categories: proxy
---

```sh
#!/usr/bin/env python
from scapy.all import *

def arp_monitor_callback(pkt):
  if ARP in pkt:
    pkt[ARP].remove_payload()
    return pkt[ARP].summary()
  if pkt[ARP].op == 2: # Is at
    return pkt.sprintf("%ARP.psrc% is at %ARP.hwsrc% => %ARP.pdst%")
  elif pkt[ARP].op == 1: # who has
    return pkt.sprintf("Who has %ARP.pdst% tell %ARP.psrc%")

sniff(prn=arp_monitor_callback, filter="arp", store=0)
```
