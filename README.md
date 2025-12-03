# 🐧Yocto Linux Kernal Build for Raspberry_Pi_3
Contains Yocto Configuration files, custom layer settings, and build outputs for creating a lightweight embedded linux system on Raspberry Pi 3

## Project Overview
* **Target Devive:** Raspbery Pi 3 B
* **Build System:** Yocto Project
* **Host OS:** Ubuntu 22.04 LTS
* **Yocto Version:** Kirkstone

## Details
* **Open Enbedded:** Build system and community
* **Yocto Project:** Umbrella project and community
* **Metadata:** files containing information about how to build an image
* **Recipe:** file with instructions to build one or more packages
* **Layers:** directory containing grouped metadata (start with "meta-")
* **Board support package (BSP):** layer that defines how to build for board (usually maintained by vendor
* **Distribution:** specific implementation of Linux (kernel version, rootfs, etc.)
* **Machine:** defines the architecture, pins, buses, BSP, etc
* **Image:** output of build process (bootable and executable Linux OS)

  **Poky = BitBake + Metadata**
* **Poky:** Build System used by Yocto Project
* **BitBake:** A task executor and scheduler

## Yocto Installation Flow 
 **Clone poky kirkstone** ⇨ **Clone Layer meta-raspberrypi** ⇨ **Create Build Directory using env** (Initialize Build Environment) ⇨ **Edit bblayers.conf** (Add BSP Layer) ⇨ **Edit local.conf** (machine, Uart, SSh) ⇨ **Bitbake core-image-minimal** (Build) ⇨ **Flash** 

## Installation Procedure
### Install Prerequisites
```sh
$ sudo apt-get install gawk wget git-core diffstat unzip \
texinfo gcc-multilib build-essential chrpath zstd
```
### Clone the Yocto Layers
Create a sources directory and include these layers
#### 1. Poky (core layer and build system)
```sh
$ mkdir sources
$ cd sources/
$ git clone git://git.yoctoproject.org/poky -b Kirkstone
```
#### 2. meta-raspberrypi (BSP layer)
```sh
$git clone git://git.yocyoproject.org/meta-raspberrypi -b Kirkstone
```
### Configuration
Go to your initial directory (in my case its Yocto) & run this command to create a dedicated environment.
```sh
$ source sources/poky/oe-init-build-env
```
Navigate to build directory
```sh
$ cd build/conf/
$ vi bblayers.conf
```
Setup bblayers.conf
```sh
# POKY_BBLAYERS_CONF_VERSION is increased each time build/conf/bblayers.conf
# changes incompatibly
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BBFILES ?= ""

BBLAYERS ?= " \
  /home/labuser/Desktop/yocto/sources/poky/meta \
  /home/labuser/Desktop/yocto/sources/poky/meta-poky \
  /home/labuser/Desktop/yocto/sources/meta-raspberrypi \
  "
```
Configure local.conf
```sh
MACHINE ??= "raspberrypi3"
EXTRA_IMAGE_FEATURES:append = " ssh-server-openssh"
```
Configure 

$
###
$ cd ..
$ source sources/poky/oe-init-build-env
$ vi conf/bblayers.conf

##Custom Layer
```sh
bitbake-layers create-layer meta-mylayer
cat /proc/sys/fs/inotify/max_user_instances 
cat /proc/sys/fs/inotify/max_queued_events 
cat /proc/sys/fs/inotify/max_user_watches 
```
###Issue
```sh
cat /proc/sys/fs/inotify/max_queued_events 
sudo sysctl -w fs.inotify.max_queued_events=32768
echo "fs.inotify.max_queued_events=32768" | sudo tee -a /etc/sysctl.conf 
sudo sysctl -p
pkill -9 bitbake
pkill -9 bitbake-server
pkill -9 bitbake-worker


bitbake-layers create-layer meta-mylayer
bitbake-layers show-layers
bitbake-layers add-layer ../meta-mylayer
```
