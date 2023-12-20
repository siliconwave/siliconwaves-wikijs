---
title: Installation Steps
description: 
published: true
date: 2023-12-20T07:35:19.168Z
tags: 
editor: markdown
dateCreated: 2023-12-20T06:12:44.289Z
---

## Step 1: Select boot mode
Choose the correct boot mode based on the storage medium. In our case, select boot mode as SDIO Boot.
![star-v.png](/star-v.png)
## Step 2: Downloading the Debian OS Image
Visit Website Link to download the VisionFive 2 Debian OS image using the provided command:

    curl −O <Website Link>
## Step 3: Flashing the OS to SD Card
- Utilize BalenaEtcher to flash the OS onto an SD card following the outlined steps:
- Insert a micro-SD card into your computer's micro-SD card reader or a built-in card reader on a laptop.
Extract the .bz2 file:

      zip2 -dk [filename].img.bz2
- Download and install BalenaEtcher software from: https://www.balena.io/etcher/
- Open BalenaEtcher.
- Click on 'Flash from file' and select the location of the image you extracted:

      starfive-jh7110-VF2-[Version].img
- Click 'Flash!' to start the flashing process.
## Step 4: Insert the SD card and power on.
## Step 5: Use the following login credentials:
- User: user
- Password: starfive