---
title: Installation Steps
description: 
published: true
date: 2023-12-19T12:41:30.207Z
tags: 
editor: markdown
dateCreated: 2023-12-19T12:25:52.938Z
---

## Prerequisites

    sudo apt update
    sudo apt install build-essential clang flex bison g++ gawk gcc-multilib g++-multilib \
    gettext git libncurses-dev libssl-dev python3-distutils rsync unzip zlib1g-dev \
    file wget

## Image Build Steps
Starfive tech team shared steps to build openWRT image 

https://www.dropbox.com/scl/fi/s06gpwtbifn89rsagdy5o/Compile-and-Install-OpenWrt-on-VisionFive-2_Preliminary.pdf?rlkey=g9xdnfbrw7k8msp6wdlcrh99y&dl=0

## 1. Clone the OpenWRT starfive board repository:
       git clone https://git.openwrt.org/openwrt/staging/wigyori.git
       cd wigyori/
       git checkout riscv-jh71x0-202308b
       make menuconfig
## 2. Checkout to the StarFive board specific branch
       git checkout riscv-jh71x0-202308b
## 3. Initiate the Build Configuration
       make menuconfig

- Select the following configurations:
- Board configuration:
- Select -> Target System as (StarFive JH71x0 (7100/7110))
- Select -> Target Profile (StarFive VisionFive 2 v1.3b)
- Select -> Target Image 
  - -> Select -> Root filesystem archives
  - -> Select -> ext4, Gzip images, cpio.gz
## 4. Exit the configuration 
## 5. Install luci
     ./scripts/feeds update packages luci
     ./scripts/feeds install -a -p luci
## 6. Enter the menu configuration GUI to configure luci:
     make menuconfig
###  Luci configuration:
  - Select ? Network
    - Select ? Web Servers/Proxies
      - Select -> uhttpd
  - Select ? LuCI
    - Select -> 1. Collections
      - Select -> luci
    - Select -> 3. Applications
      - Select -> luci-app-ddns, luci-app-fire, luci-app-ntpc, luci-app-samba4, luci-app-uhttpd
    - Select -> 4. Themes
      - Select all
### Wireless Configuration:
  - Select -> Kernel modules
    - Select -> Wireless Driver
      - Select -> kmod-cfg80211, kmod-mac80211, kmod-rtl8821ae
   - Select -> Network
     - Select -> WirelessAPD
        - Select -> wpad-basic-mbedtls, hostapd-common, wpa-cli, hostapd-utils
## 7. Exit the configuration 
## 8. Download the dependency packages
       ./scripts/feeds update -a
       ./scripts/feeds install -a
         make download V=s
## 9. Add passwall function:
        echo "src-git passwall_packages https://github.com/xiaorouji/openwrt-passwall-packages.git;main" >> "feeds.conf.default"
        echo "src-git passwall https://github.com/xiaorouji/openwrt-passwall.git;main" >> "feeds.conf.default"
Modify include/target.mk:
        
![](https://paper-attachments.dropboxusercontent.com/s_5F0001FEBC3908E38B9A03266DC1F4B0F3C06C977965A8108FDC989461150BE5_1702546651242_image.png)

- Run

       ./scripts/feeds update -a
       ./scripts/feeds install -a
       ./scripts/feeds install -a -f -p PWpackages
       ./scripts/feeds install luci-app-passwall
- Configure passwall and unconfigure dnsmasq:

        make menuconfig

### Luci configuration:
   - Select -> Applications
     - Select ->  luci-app-passwall
### Base system
- Select -> dnsmasq
- Select -> dnsmasq-full
- Execute the following command to update and download software package:

         make download V=s
## 10. To compile:

          make -j8
## 11.  Update SPL and U-boot in board Using Debian Image 
-  Download  SPL and U-boot by the  below link.

       https://github.com/starfive-tech/VisionFive2/releases/tag/VF2_v3.4.5
     
![](https://paper-attachments.dropboxusercontent.com/s_99C54FDEE4AD8B70FC830657C7CCF9E4F48149BB8987BB12E8A052786A5C0488_1696525839217_file.png)

- Use debian image boot from sd card boot mode, and then use flashcp to update
- Follow the flashcp steps in the below document
        https://doc-en.rvspace.org/VisionFive2/Quick_Start_Guide/VisionFive2_SDK_QSG/spl_new.html
## 12. Flash on SD card image:
- Generated openWRT path

       bin/targets/jh71x0/generic
- filename : openwrt-jh71x0-generic-visionfive2-v1.3b-ext4-sdcard.img.gz
    To unzip image

       gunzip openwrt-jh71x0-generic-visionfive2-v1.3b-ext4-sdcard.img.gz
    To flash on sd card

       dd if=openwrt-jh71x0-generic-visionfive2-v1.3b-ext4-sdcard.img of=/dev/sdX bs=1M oflag=direct


## 13. Installation openWRT in board
    - Insert the SD card into the board and turn both boot mode switches to the low position, which is QSPI NOR flash.
    
![](https://paper-attachments.dropboxusercontent.com/s_5F0001FEBC3908E38B9A03266DC1F4B0F3C06C977965A8108FDC989461150BE5_1702550073370_image.png)

- Use the 'apprate' serial converter to check the logs on the board. We using the serial converter, refer to the following link.
- Connect the TX of the board to the RX of the serial connector and connect the RX of the board to the TX of the serial connector. Also, connect the GND and 5V.
![](https://paper-attachments.dropboxusercontent.com/s_5F0001FEBC3908E38B9A03266DC1F4B0F3C06C977965A8108FDC989461150BE5_1702551024869_file.png)

- Use the CoolTerm application to check the logs. Download the application from this link:  
- https://www.dropbox.com/scl/fi/pr5alk18i4fqgtkg6icrf/CoolTermLinux64Bit.zip?rlkey=0hcppt06lhz9q6ksnfiorh4um&dl=0
- Open the CoolTerm application, select the correct USB connection to which the serial port is connected, set the baud rate to 11520, and start the connection with the serial port.
- Now, you can view the logs of the OpenWRT installation. The system will successfully boot, and by default, you will be in the root login.
