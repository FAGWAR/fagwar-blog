---
title: "Coreboot T480"
date: 2025-04-20T22:46:00+01:00
draft: true
---

## Requirements

- A ThinkPad T480

- A bios programmer with clip (CH341a, Raspberry Pi (pico))

- A computer running GNU/Linux

- A screwdriver

## Step 1. Update the bios on your T480 using a USB stick

### Making a bootable bios update USB

Go to [this page](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t480-type-20l5-20l6/downloads/ds502355) and download the latest iso availabe.

Download eltorito from GitHub.

``curl -LO https://github.com/rainer042/geteltorito/raw/refs/heads/main/geteltorito.pl``

make it executable

``chmod +x geteltorito.pl``

Make a bootable img from the iso

``./geteltorito -o bios.img /path/to/image.iso``

Find your USB stick using lsblk
```
                          [I] ye@desktop ~ [127]> lsblk
                          NAME        MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINTS
Most likely this one ->   sda           8:0    1 14.3G  0 disk  
                            ├─sda1        8:1    1  512M  0 part  
                            └─sda2        8:2    1 13.8G  0 part  
                            zram0       253:0    0  7.8G  0 disk  [SWAP]
                            nvme0n1     259:0    0  1.8T  0 disk  
                            ├─nvme0n1p1 259:1    0    1G  0 part  /boot
                            └─nvme0n1p2 259:2    0  1.8T  0 part  
                              └─root    254:0    0  1.8T  0 crypt /home
                          [I] ye@desktop ~>
```

Burn it to a USB stick

``dd if=bios.img of=/dev/sdX bs=1M status=progress conv=fsync``

### Installing the BIOS update from usb

***Make sure your laptop is plugged in and charging, with a battery connected***

Turn on your T480 and spam the <**F12**> key

< add picture of boot menu >

Choose your USB stick from this list. It should boot into a screen like 

< add picture of bios update tool >


## Step 2. Take apart your T480

Take out your battery and all of the screws at the bottom of the laptop

< picture of screws highlighted and battery taken out >

Take off the bottom case, it's held in with clips - so use a spudger and be careful taking it off or you *will* snap some off them off

< picture of bottom of laptop >


## Step 3. Dump your bios

Put the clip 


