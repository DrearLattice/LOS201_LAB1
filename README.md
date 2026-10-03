# Embedded Linux Lab 1

## 1. Overview

This project is the implementation of Embedded Linux Lab 1.

The main objectives are:

- Build the Linux kernel for ARM.
- Build BusyBox for ARM.
- Build U-Boot for the VExpress A9 board.
- Create an ARM root filesystem.
- Create an initramfs image.
- Boot Embedded Linux using QEMU.
- Boot Embedded Linux through U-Boot.
- Verify the complete boot process.

## 2. Environment

- Host: Ubuntu Linux
- Cross compiler: arm-linux-gnueabihf-gcc-11
- Architecture: ARMv7
- Target machine: VExpress A9
- CPU: Cortex-A9
- Memory: 512 MB
- Linux kernel: 5.15
- BusyBox: 1.35.0
- U-Boot: 2022.04
- Emulator: QEMU

## 3. Project Structure

```text
embedded-linux-lab1/
├── README.md
├── .gitignore
├── configs/
│   ├── kernel.config
│   ├── busybox.config
│   └── uboot.config
├── output/
│   ├── zImage
│   ├── u-boot
│   ├── vexpress-v2p-ca9.dtb
│   └── initramfs.cpio.gz
├── rootfs/
│   ├── bin/
│   │   └── busybox
│   ├── etc/
│   │   ├── hostname
│   │   ├── inittab
│   │   ├── passwd
│   │   └── init.d/
│   │       └── rcS
│   └── init
├── report/
└── screenshots/
```

## 4. Main Components

### Linux Kernel

The Linux kernel was configured and built for the ARM architecture.

Final kernel image:

```text
output/zImage
```

### BusyBox

BusyBox provides the basic Linux utilities used by the ARM root filesystem.

Final BusyBox binary:

```text
rootfs/bin/busybox
```

### Root Filesystem

The root filesystem contains the required configuration files, initialization scripts, hostname, password file, and BusyBox.

Main initialization file:

```text
rootfs/init
```

### U-Boot

U-Boot was built for the VExpress A9 platform.

Final U-Boot image:

```text
output/u-boot
```

### Device Tree

The VExpress A9 Device Tree Blob is:

```text
output/vexpress-v2p-ca9.dtb
```

### Initramfs

The compressed initramfs image is:

```text
output/initramfs.cpio.gz
```

## 5. Boot Methods

### 5.1 Direct Kernel Boot with QEMU

The Linux kernel can be booted directly using QEMU:

```bash
cd ~/embedded_lab1

qemu-system-arm \
    -M vexpress-a9 \
    -cpu cortex-a9 \
    -m 512M \
    -kernel output/zImage \
    -dtb output/vexpress-v2p-ca9.dtb \
    -initrd output/initramfs.cpio.gz \
    -append "console=ttyAMA0,115200 rdinit=/sbin/init mem=512M" \
    -nographic \
    -smp 2
```

A successful boot reaches the BusyBox shell and displays the Embedded Linux Lab 1 banner.

### 5.2 Boot through U-Boot

The final U-Boot boot command was:

```text
bootz 0x61000000 0x63000000:1084559 0x62000000
```

Memory addresses:

```text
0x61000000 - Linux zImage
0x62000000 - Device Tree Blob
0x63000000 - initramfs
```

U-Boot successfully loaded the kernel, Device Tree, and initramfs before starting Linux.

## 6. Verification

The following components were verified:

- Linux kernel successfully built for ARM.
- BusyBox successfully built for ARM.
- U-Boot successfully built.
- Root filesystem successfully created.
- Initramfs successfully created.
- Linux successfully booted using QEMU.
- Linux successfully booted through U-Boot.
- BusyBox shell successfully started.
- Hostname was configured as `embedded-arm`.

The final initramfs image was also verified using SHA-256:

```text
3dd79d1e0fcb19c3a6b2adf8c64d96e44e4f2df82e52ca113eac30d30d88591c
```

## 7. Result

The Embedded Linux Lab 1 environment was successfully completed.

The final system can boot an ARM Linux kernel on the VExpress A9 platform using QEMU.

The boot process was verified using:

1. Direct kernel boot.
2. U-Boot boot.

The BusyBox-based root filesystem successfully started and provided an interactive shell.

## 8. Report

The detailed lab report and screenshots can be added to:

```text
report/
screenshots/
```

The report contains the detailed implementation steps, configuration, testing process, and results.
