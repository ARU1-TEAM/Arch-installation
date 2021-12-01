## Table of Contents

* [Introduction](#introduction)
* [Install Arch](#install-arch)
  * [Create USB Flash](#create-usb-flash)
  * [Boot On USB Flash](#boot-on-usb-flash)
  * [Change Keyboard Layout](#change-keyboard-layout)
  * [Check Internet Connection](#change-internet-connection)
  * [Set The Time](#set-time)
  * [Creating Partitions](#creating-partitions)
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
If you don't know what disk you want to install Arch on, Type this.
~~~ sh
fdisk -l
~~~
Now that you know which disk you are using (in our case, `sda`) we can run this to select the disk and create the partitions
~~~ sh
fdisk /dev/sda
~~~
