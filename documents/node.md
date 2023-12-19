---
title: Build Steps for Node.js on OpenWRT
description: 
published: true
date: 2023-12-19T11:13:14.372Z
tags: 
editor: markdown
dateCreated: 2023-12-19T11:13:14.372Z
---




# Prerequisites:

- Ensure you have a toolchain for OpenWRT.

# Procedure:

## 1. Clone the Node.js repository:
     git clone https://github.com/nodejs/node.git
## 2. Checkout the v18.0.0 release:
     git checkout v18.0.0
## 3. Set the environment values:
     CC=riscv64-unknown-linux-gnu-gcc CXX=riscv64-unknown-linux-gnu-g++ CC_host=gcc CXX_host=g++ ./configure --dest-cpu=riscv64 --cross-compiling --dest-os=linux --openssl-no-asm
## 4. Compile the code:
    make -j$(nproc) # This may take 2-3 hours
    make install PREFIX=./install
- The output files will be located in the './install' directory.
## 5. Copy the 'install' file to the RISC-V board:
    scp install root@<ip-address>:.
## 6. Copy the 'install' folder to /usr:
    cp install /usr/
## 7. Add Node.js to the profile path:
    echo 'export PATH=/usr/install/bin:$PATH' >> /etc/profile
## 8. Test the Node.js version:
    $ node -v
