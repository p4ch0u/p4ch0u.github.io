---
layout: post
title: "Setup a proxy SOCKS using ssh tunnel"
date: 2017-05-17 00:00:50 +0200
categories: proxy
---

Open a terminal and run this command to add the group allowed to setup a tunnel

{% highlight sh %}
addgroup allow_tunnel
{% endhighlight %}

In /etc/ssh/sshd_config, add or replace the following lines at the end of the file

```sh
Match Group allow_tunnel
  AllowTcpForwarding yes
  AllowAgentForwarding yes
  X11Forwarding no
  PermitTunnel yes
  GatewayPorts yes
  #PermitOpen localhost:1080
  ForceCommand echo 'This account can only be  used for SOCKS and has be restricted accordingly.'
```

Create a `user` for the tunnel and add it to “allow_tunnel” group.

```sh
useradd $USER_tun
usermod -a -G allow_tunnel -s /usr/bin/tunnel_shell $USER_tun
```

Note: You cannot allow tunnel usage for a user that may not log into ssh.

Create a new file and make it executable

```sh
touch /usr/bin/tunnel_shell
chmod +x /usr/bin/tunnel_shell
```

Edit the file you just created with vim (“vim /usr/bin/tunnel_shell“)

```sh
#!/bin/bash
trap '' 2 20 24 # CTRL+Z will escape from the script giving you full access to bash… Try adding << trap '' 20 >>
clear
echo -e "\r\n \e[5m \e[43m \e[31mSSH tunnel started, shell disabled by the syste$m administrator\e[0m \r\n"
while [ true ] ; do
 sleep 1000
done
exit 0

# Number SIG     Meaning
# 0      0       On exit from shell
# 1      SIGHUP  Clean tidyup
# 2      SIGINT  Interrupt
# 3      SIGQUIT Quit
# 6      SIGABRT Abort
# 9      SIGKILL Die Now (cannot be trap'ped)
# 14     SIGALRM Alarm Clock
# 15     SIGTERM Terminate
```

Add the fresh shell to the list in your server

```sh
echo "/usr/bin/tunnel_shell" >> /etc/shells
```

Restart the ssh service

```sh
systemctl restart sshd
```
