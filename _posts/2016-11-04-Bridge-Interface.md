---
layout: post
title: "Bridge interface"
date: 2016-11-04 00:00:50 +0200
categories: proxy
---

Ajout des interfaces au bridge

```sh
#!/bin/sh

BRCTL=/sbin/brctl
IP=/bin/ip
BR=$1
shift
clear_if_addr () {
  sudo $IP addr flush dev $1
}
add_if_to_br () {
  sudo $BRCTL addif $1 $2
}
sudo $BRCTL addbr $BR
sudo $BRCTL stp $BR on
for i in $*
do
  clear_if_addr $i
  add_if_to_br $BR $i
done
$BRCTL show
```

Suppression du bridge des interfaces

```sh
#!/bin/sh

BRCTL=/sbin/brctl
IP=/bin/ip
AWK=/usr/bin/awk
BR=$1
get_ifs_in_br () {
  $BRCTL show $1 | $AWK '(NR>1){print $NF}'
}
del_all_ifs_in_br () {
  sudo $BRCTL delif $1 $(get_ifs_in_br $1)
}
del_all_ifs_in_br $BR
sudo $IP link set $BR down
sudo $BRCTL delbr $BR
$BRCTL show
```
