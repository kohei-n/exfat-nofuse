exfat-nofuse
============

Fork of https://github.com/dorimanx/exfat-nofuse
Linux Kernel Driver for exfat, also compatible with the latest linux kernel 5.0 and newer.

Installing as a DKMS module:
=================================

Then copy the root of this repository to /usr/src

	sudo cp -R . /usr/src/exfat-1.2.9
	sudo dkms add -m exfat -v 1.2.9
	sudo dkms build -m exfat -v 1.2.9
	sudo dkms install -m exfat -v 1.2.9

Now you have a proper dkms module that will work for a long time... hopefully.


Installing as a stand-alone module:
====================================

    make
    sudo make install

To load the driver manually, run this as root:

    modprobe exfat

Installing as a part of the kernel:
======================================

Let's take [linux] as the path to your kernel source dir...

	cd [linux]
	cp -rvf exfat-nofuse [linux]/fs/exfat

edit [linux]/fs/Kconfig
```
 menu "DOS/FAT/NT Filesystems"

  source "fs/fat/Kconfig"
 +source "fs/exfat/Kconfig"
  source "fs/ntfs/Kconfig"
  endmenu
```
  

edit [linux]/fs/Makefile
```
  obj-$(CONFIG_FAT_FS)    += fat/
 +obj-$(CONFIG_EXFAT_FS)  += exfat/
  obj-$(CONFIG_BFS_FS)    += bfs/
```

	cd [linux]
	make menuconfig

Go to:
> File systems > DOS/FAT/NT
>   check exfat as MODULE (M)
>   (437) Default codepage for exFAT
>   (utf8) Default iocharset for exFAT

> ESC to main menu
> Save an Alternate Configuration File
> ESC ESC

build your kernel

Have fun.


