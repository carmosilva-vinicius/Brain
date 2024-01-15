Boot are one of directory of [[Directory structure#Root|root]] Linux directories. It has the binaries that is responsible for the system initialization. The `vmlinuz` files are the kernel binary, which are the first binary that are executed at the system start. After this, the `initram` are executed.

There we can see two kernel versions. So we can have various kernel versions installed and decide between then which one will be used to start the system.
```sh
user@manjaro /$ sudo ls -la boot

total 142504
drwxr-xr-x  5 root root     4096 jan 13 12:57 .
drwxr-xr-x 20 root root     4096 jan 13 12:56 ..
-rw-r--r--  1 root root    81920 dez 11 12:32 amd-ucode.img
drwx------  3 root root     4096 dez 31  1969 efi
drwxr-xr-x  6 root root     4096 jan 13 12:57 grub
-rw-------  1 root root 45053741 jan 13 12:57 initramfs-5.15-x86_64-fallback.img
-rw-------  1 root root 16121311 jan 13 12:56 initramfs-5.15-x86_64.img
-rw-------  1 root root 45870296 jan 13 12:57 initramfs-6.1-x86_64-fallback.img
-rw-------  1 root root 16311554 jan 13 12:57 initramfs-6.1-x86_64.img
-rw-r--r--  1 root root       23 jan  5 13:19 linux515-x86_64.kver
-rw-r--r--  1 root root       21 jan  5 13:20 linux61-x86_64.kver
drwxr-xr-x  2 root root     4096 jan 13 12:56 memtest86+
-rw-r--r--  1 root root 10830752 jan 13 12:56 vmlinuz-5.15-x86_64
-rw-r--r--  1 root root 11610144 jan 13 12:56 vmlinuz-6.1-x86_64
```

- `amd-ucode.img`: This file contains microcode updates for AMD CPUs. The Linux kernel can update the CPU's firmware during boot using this image [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `efi`: This directory is part of the EFI (Extensible Firmware Interface) system partition that stores boot loader files for systems using UEFI (Unified Extensible Firmware Interface) [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `grub`: This directory contains files for the GRUB (GRand Unified Bootloader) bootloader, including its configuration files and modules necessary for the boot process [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `initramfs-5.15-x86_64-fallback.img` and `initramfs-6.1-x86_64-fallback.img`: These files are fallback initial ramdisk images. An initramfs is a temporary root file system loaded into memory as part of the Linux boot process. The fallback image may contain additional drivers and modules to ensure booting in case the standard initramfs fails [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `initramfs-5.15-x86_64.img` and `initramfs-6.1-x86_64.img`: These are the standard initial ramdisk images for their respective kernel versions. They contain the minimal set of files and drivers needed to mount the actual root file system during the boot process [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `linux515-x86_64.kver` and `linux61-x86_64.kver`: These files likely contain the version information for the respective Linux kernel versions [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `memtest86+`: This directory contains the files necessary to run Memtest86+, a software utility that tests the computer's memory for errors [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).
- `vmlinuz-5.15-x86_64` and `vmlinuz-6.1-x86_64`: These files are the Linux kernel itself. The vmlinuz file is a compressed, bootable Linux kernel image [4](https://www.tecmint.com/linux-directory-structure-and-important-files-paths-explained/).