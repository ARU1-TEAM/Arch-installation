## Table of Contents

* [Introduction](#introduction)
* [Install Arch](#install-arch)
  * [Create USB Flash](#create-usb-flash)
  * [Boot On USB Flash](#boot-on-usb-flash)
  * [Change Keyboard Layout](#change-keyboard-layout)
  * [Check Internet Connection](#change-internet-connection)
  * [Set The Time](#set-time)
  * [Creating Partitions](#creating-partitions)
  * [Base Installation](#base-installation)
  * [Set Time-Zone](#set-time-zone)
* [Install Packages](#install-packages)
  * [Primary Packages](#primary-packages)
  * [Side Applications](#side-applications)
  * [Terminal Applications](#terminal-applications)
* [Install Xfce](#install-xfce)
  * [Xubuntu-Desktop](#xubuntu-desktop)
  * [Uninstall Xfce](#uninstall-xfce)
* [Customize Xfce](#customize-xfce)
  * [Window Theme](#window-theme)
  * [Icon Theme](#icon-theme)
  * [Cursor Theme](#cursor-theme)
  * [Fonts](#fonts)
  * [Panel Preferences](#panel-preferences)
* [Customize Terminal](#customize-terminal)
  * [PowerLevel10k](#powerlevel10k)
  * [Customize Terminal Theme](#customize-terminal-theme)
* [Install I3wm](#custom-i3wm)

## Introduction
This repository is made to help you in the complete installation of Arch. At the end of this repo you will get a nice xfce4 fully nord customized on your Arch followed by I3wm and all it's customization as well. 

## Install Arch 
<p align="center"><img src="arch_logo.png" alt="ubuntu"></p>

### Create USB Flash
- Download [Arch iso file](https://archlinux.cu.be/iso/2021.12.01/) and select the `archlinux-2021.12.01-x86_64.iso`.
- Download [balenaEtcher](https://www.balena.io/etcher/).
- Load balena etcher, put iso file and select your usb key.
- 
### Boot On USB Flash
 - Reboot your computer and press `DEL` key to get into your BIOS/UEFI.
 - Select your usb-key in the boot menu.
 - Save and exit.
 - 
### Change Keyboard Layout
The first thing to do is to change the keyboard layoutsi it won't bother us for the rest of the installation. To change it in french use this command
~~~ sh
loadkeys fr-latin1

~~~
### Check Internet Connection
We will also check if we are connected so we can install all the needed packages later. To do so, type this command
~~~ sh 
ping google.com
~~~
If there are mutliple entries going without stopping, that's great !
You can do `ctrl+c` to stop the command

### Set The Time
You can easaly set the time by running this command 
~~~ sh
timedatectl set-ntp true
~~~
You can check the time to see if it worked using 
~~~ sh
timedatectl status
~~~

### Creating Partitions 
WARNING: pay attention to the following instructions, this will erase everything that's on your disk. 

First we will select the disk you want to install Arch on.
If you don't know what disk you want to install Arch on, Type this.
~~~ sh
fdisk -l
~~~
Now that you know which disk you are using (in our case, `sda`) we can run this to select the disk.
~~~ sh
fdisk /dev/sda
~~~
 
Now we can create the partitions.
- First type `g` to create a new empty GTP partition table
- Then type `n` to create a new partition. You can leave everything by default (by pressing `enter`) here except the last sector. You will type `+550M` for the last sector. Then press `enter`
- Then type `n` again. Leave the two first option by default like the first one. And type `+2G` for the last sector. Then press `enter`
- Then type `n` again. And for this one, you can leave everything by default (the last sector will automatically take all the remaining space). So just press `enter` 3 times. 

Now we will change the partitions format
- First type `t` and select the partition 1 by typing `1` to change it's format. And then type `1` again to change the first partition format into EFI
- Type `t` again and this time type `2` to select the second partition. Then type `19` to put the second partition format in linux_swap

And finally we will type `w` to write all the changes and exit fdisk.

The EFI partition needs to be FAT32 so enter this command 
~~~ sh
mkfs.fat -F32 /dev/sda1
~~~
Let's configure the swap now by doing 
~~~ sh
mkswap /dev/sda2
~~~
Followed by
~~~ sh
swapon /dev/sda2
~~~
And now let's make the filesystem table by doing 
~~~ sh
mkfs.ext4 /dev/sda3
~~~
Now we have to mount the filesystem partiton with
~~~ sh
mount /dev/sda3 /mnt
~~~

### Base Installation
First we will install pacstrap, the base kernel installation
~~~ sh
pacstrap /mnt base linux linux-firmware
~~~
Now we will install fstab (Don't know what that is for the moment)
~~~ sh
genfstab -U /mnt >> /mnt/etc/fstab
~~~
And now we can go in the root file to continue the rest of the installation using 
~~~ sh
arch-chroot /mnt
~~~
The prompt has normally changed now. 

### Set Time-Zone
We will now set our time zone using this command. We will select brussels for this example but change it of course
~~~ sh 
ln -sf /usr/share/zoneinfo/Europe/Brussels /etc/localtime
~~~
Set the hardware clock using 
~~~ sh
hwclock --systohc
~~~

