---
title: Release Notes
description: 
published: true
date: 2023-12-20T07:42:43.910Z
tags: 
editor: markdown
dateCreated: 2023-12-20T07:25:59.027Z
---

# Release Notes
- Linux Kernel: 5.15.0 (StarFive kernel tag v3.1.5),
- U-boot: StarFive uboot tag v3.1.5 ,
- Debian Snapshot date: 20221225T084846Z (sid)

## Gnome Wayland Default Windowing System
- Gnome Wayland serves as a default windowing system right from start of the Release.
## Upgrade Note: apt upgrade Avoidance
- Avoid using apt upgrade to prevent overriding customized mesa and linux-libc-dev versions.
## Generic
- NVMe PCIe boot image provided; Set QSPI boot mode. (Refer to "Boot Mode Settings").
- Pink screen overlay issue fixed.
- Support for resolutions like 2K and 1024x728 are added
## Packages
- Imagination DDK upgraded from version 1.17 to 1.19
- Mesa updated from version 21.3.8 to 22.3.5
## Miscellaneous
- Audio devices in Gnome Desktop renamed to "Audio Jack" and "HDMI Audio.
- Made installation of libicu71 as Default
- Libreoffice performance improved with GTK3