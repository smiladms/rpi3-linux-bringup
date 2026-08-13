# rpi3-linux-bringup

An Embedded Linux operating system built entirely from scratch for the Raspberry Pi 3 Model B. 

This project bypasses automated build systems (like Buildroot or Yocto) to demonstrate a deep, low-level understanding of the embedded Linux boot stack, cross-compilation, hardware initialization, and root filesystem construction.

## 🚀 Architecture & Tech Stack
* **Target Hardware:** Raspberry Pi 3 Model B (BCM2837 SoC)
* **Architecture:** AArch64 (64-bit ARM Cortex-A53)
* **Toolchain:** Custom GCC cross-compiler built with Crosstool-NG
* **Bootloader:** Das U-Boot (compiled from source, utilizing custom boot scripts)
* **Kernel:** Mainline Linux Kernel v6.6 (`defconfig` for `arm64`, custom `bcm2837-rpi-3-b.dtb` device tree)
* **Root Filesystem:** Built from scratch using statically-linked BusyBox
* **Storage:** Persistent `ext4` block filesystem running from a partitioned SD Card
* **Init System:** Custom SysVinit (`inittab` and `rcS` scripts)

## 🛠️ Implementation Details
This repository highlights the critical boot path and initialization scripts required to bring up the hardware from bare metal to a user shell:

1. **Bootloader Configuration:** Custom `boot.scr` deployed to load the kernel and device tree into RAM, and to dynamically pass boot arguments (`root=/dev/mmcblk0p2 rootfstype=ext4 rw rootwait`) to the kernel.
2. **User Space Initialization:** SysVinit configuration (`inittab`) configured to bootstrap the system, execute startup scripts (`rcS`) to mount virtual filesystems (`/proc`, `/sys`, `devtmpfs`), and spawn a serial console (`ttyS1`).
3. **Storage Migration:** Successfully transitioned the root filesystem from a volatile RAM disk (`initramfs`) to a persistent block device for long-term data retention.

## 📁 Repository Files
*(I recommend copying your custom `boot.txt`, `rcS`, and `inittab` files from your Ubuntu machine into this folder so hiring managers can actually read the code you wrote!)*

## 📸 

<img width="949" height="1280" alt="photo_2026-08-14_01-54-42" src="https://github.com/user-attachments/assets/f65c6c10-7de7-433b-9fd0-9b94308d0e44" />
