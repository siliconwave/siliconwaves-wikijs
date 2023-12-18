---
title: Installing ssh server in Board 
description: 
published: true
date: 2023-12-18T12:54:37.310Z
tags: 
editor: markdown
dateCreated: 2023-12-18T12:54:37.310Z
---

https://www.dropbox.com/scl/fi/s0d1houfhgteqihj1f59g/openwrt-jh71x0-generic-visionfive2-v1.3b-ext4-sdcard.img?rlkey=ex40vyevffpxxtfdrxyttnfnt&dl=0


----------
# Installing ssh server in Board 
## 1. Initially, the opkg download path will be incorrect. To override the content, use the following command in :

        echo -e 'src/gz openwrt_core https://downloads.openwrt.org/snapshots/packages/riscv64_riscv64/packages/\nsrc/gz openwrt_base https://downloads.openwrt.org/snapshots/packages/riscv64_riscv64/base/\nsrc/gz openwrt_passwall https://downloads.openwrt.org/snapshots/packages/riscv64_riscv64/packages/\nsrc/gz openwrt_passwall_packages https://downloads.openwrt.org/snapshots/packages/riscv64_riscv64/base/' | tee /etc/opkg/distfeeds.conf > /dev/null
## 2. Update opkg:

       opkg update
## 3. Install SSH server:

       opkg install openssh-server
## 4. Check the status of ssh server

       /etc/init.d/sshd status
## 5. Initially, port 22 will point to dropbear, so stop dropbear and restart the SSH server
>     Note :Dropbear is a lightweight SSH server, while OpenSSH has more features than Dropbear. It offers additional options, such as support for SFTP
{.is-info}


       /etc/init.d/dropbear stop
       /etc/init.d/sshd restart
## 6. Update the firewall

       uci add firewall rule
       uci set firewall.@rule[-1].name='Allow-SSH'
       uci set firewall.@rule[-1].src='*'
       uci set firewall.@rule[-1].proto='tcp'
       uci set firewall.@rule[-1].dest_port='22'
       uci set firewall.@rule[-1].target='ACCEPT'
       uci commit firewall
    # firewall for port 80 to access the luci GUI 
    uci add firewall rule
    uci set firewall.@rule[-1].name='Allow-HTTP'
    uci set firewall.@rule[-1].src='*'
    uci set firewall.@rule[-1].proto='tcp'
    uci set firewall.@rule[-1].dest_port='80'
    uci set firewall.@rule[-1].target='ACCEPT'
    uci commit firewall

       /etc/init.d/firewall restart
## 7. Change the root permission

       sed -i 's/^#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && /etc/init.d/sshd restart
## 8. Update the root password

       passwd 
- add new password
## 9. Now you can log in to the board using the SSH server