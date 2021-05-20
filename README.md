# Nvidia Jetson Nano | Arch Linux | Volt.cx


## Table of contents
* [General info](#general-info)
* [Need for](#need-for)
* [PreInstalled](#preinstalled)
* [Build it yourself](#build-it-yourself)
* [Extra Info](#extra-info)

## General info
So i got the idea why let's not create a pre-created iso for the Nvidia Jetson Nano and post it on Github.



Arch-Nano will be available for:
* Jetson Nano (2GB)
* Jetson Nano (4GB)

## Need for
These items are needed:
* Jetson Nano
* Micro SD or USB
* balenaEtcher
* Arch-Nano

## PreInstalled
Some text will be applied here i guess.


## Build it yourself (Debian/Ubuntu)
So before we begin i use a Linux based operating system with `apt`


I love housekeeping so let's start with:
```
$ sudo apt update
$ sudo apt upgrade -y
$ sudo apt autoremove -y
$ sudo apt clean
$ sudo apt install curl wget git
```

Create a `Folder` for this project
```
$ mkdir ProjectFolder
$ cd ProjectFolder
```

Download the Nvidia Jetson Nano L4T Driver Package (BSP) and extract
```
$ wget https://developer.nvidia.com/embedded/l4t/r32_release_v5.1/r32_release_v5.1/t210/jetson-210_linux_r32.5.1_aarch64.tbz2
$ sudo tar jxpf jetson-210_linux_r32.5.1_aarch64.tbz2
$ cd Linux_for_Tegra
```

Download Arch Linux aarch64 and extract
```
$ cd rootfs
$ wget http://os.archlinuxarm.org/os/ArchLinuxARM-aarch64-latest.tar.gz
$ sudo tar -xpf ArchLinuxARM-aarch64-latest.tar.gz
```


Let's edit some files:
```
$ cd Linux_for_Tegra/nv_tools/scripts/
$ nano nv_customize_rootfs.sh
```

Find
```
    if [ -d "${LDK_ROOTFS_DIR}/usr/lib/arm-linux-gnueabihf/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/arm-linux-gnueabihf"
    elif [ -d "${LDK_ROOTFS_DIR}/usr/lib/arm-linux-gnueabi/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/arm-linux-gnueabi"
    elif [ -d "${LDK_ROOTFS_DIR}/usr/lib/aarch64-linux-gnu/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/aarch64-linux-gnu"
    else
        echo "Error: None of Hardfp/Softfp Tegra libs found"
        exit 4
    fi
```

Replace with:
```
    if [ -d "${LDK_ROOTFS_DIR}/usr/lib/arm-linux-gnueabihf/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/arm-linux-gnueabihf"
    elif [ -d "${LDK_ROOTFS_DIR}/usr/lib/arm-linux-gnueabi/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/arm-linux-gnueabi"
    elif [ -d "${LDK_ROOTFS_DIR}/usr/lib/aarch64-linux-gnu/tegra" ]; then
        ARM_ABI_DIR_ABS="usr/lib/aarch64-linux-gnu"
    elif [ -d "${LDK_ROOTFS_DIR}/usr/lib/tegra" ]; then
        ARM_ABI_DIR="${LDK_ROOTFS_DIR}/usr/lib"
    else
        echo "Error: None of Hardfp/Softfp Tegra libs found"
        exit 4
    fi
```

## Extra Info
* L4T VERSION: R32.5.1