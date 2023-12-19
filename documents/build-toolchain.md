---
title: Steps to Build C/C++ Toolchain for OpenWRT
description: the generic toolchain for RISC-V is not used, as it may not work for OpenWRT. We recommend using the SiFive toolchain
published: true
date: 2023-12-19T10:44:12.549Z
tags: 
editor: markdown
dateCreated: 2023-12-19T10:44:12.549Z
---


## 1. Download the SiFive toolchain:
    $ wget -4 https://downloads.openwrt.org/snapshots/targets/sifiveu/generic/openwrt-toolchain-sifiveu-generic_gcc-12.3.0_musl.Linux-x86_64.tar.xz
## 2. Extract the downloaded tar file:
    $ tar -xvf openwrt-toolchain-sifiveu-generic_gcc-12.3.0_musl.Linux-x86_64.tar.xz
## 3. Export the toolchain path to /usr/bin:
    $ sudo cp ~/openwrt-toolchain-23.05.0-sifiveu-generic_gcc-12.3.0_musl.Linux-x86_64/toolchain-riscv64_riscv64_gcc-12.3.0_musl/bin/r* /usr/bin