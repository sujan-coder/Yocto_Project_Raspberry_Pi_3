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
Create a source directory and include these layers
#### 1. Poky (core layer and build system)
```sh
$ git clone git://git.yoctoproject.org/poky -b Kirkstone
```
#### 2. meta-raspberrypi (BSP layer)
```sh
$git clone git://git.yocyoproject.org/meta-raspberrypi -b Kirkstone
```
#### 3. meta-openembedded (extended recipes and metadata)
```sh

$ cd ..
$ source sources/poky/oe-init-build-env
$ vi conf/bblayers.conf

