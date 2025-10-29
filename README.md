# 🐧Yocto Linux Kernal Build for Raspberry_Pi_3
Contains Yocto Configuration files, custom layer settings, and build outputs for creating a lightweight embedded linux system on Raspberry Pi 3

## Project Overview
* **Target Devive:** Raspbery Pi 3 B
* **Build System:** Yocto Project
* **Host OS:** Ubuntu 22.04 LTS
* **Yocto Version:** Kirkstone
## Installation Procedure
```sh
$ mkdir yocto

$ cd yocto

$ mkdir sources/

$ cd sources/

$ git clone git://git.yoctoproject.org/poky

$ git clone git://git.yoctoproject.org/meta-raspberrypi

$ cd ..
$ source sources/poky/oe-init-build-env
$ vi conf/bblayers.conf

