# Lab 01 report

- Student name: Maria Bogdanova
- GitHub username: mashka
- Image filename:am335x-debian-13.6-base-v6.12-armhf-2026-07-24-4gb.img.xz
- SHA-256 (paste the checksum and state whether it matches the lab):796777685b309328abcab3a122f426282c83fbde7f481ebe3e20829441f878a9

Replace each placeholder with your own command output. Label HOST and BBB
results. Do not include passwords or private keys.

## Running Linux on BBB

### BBB: `uname -r`

```text
<6.12.96-bone64>
```

### BBB: `cat /etc/os-release`

```text
<PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.6
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/">
```

### BBB: `lsblk`

```text
<NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
mmcblk0     179:0    0 29.1G  0 disk 
├─mmcblk0p1 179:1    0   36M  0 part /boot/firmware
├─mmcblk0p2 179:2    0  512M  0 part [SWAP]
└─mmcblk0p3 179:3    0 28.6G  0 part /
zram0       253:0    0  241M  0 disk [SWAP]>
```

### BBB: `ip addr`

```text
<1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether 78:04:73:41:12:65 brd ff:ff:ff:ff:ff:ff
    altname end0
    altname enx780473411265
3: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 78:04:73:41:12:68 brd ff:ff:ff:ff:ff:ff
    inet 192.168.7.2/30 brd 192.168.7.3 scope global usb0
       valid_lft forever preferred_lft forever
    inet6 fe80::7a04:73ff:fe41:1268/64 scope link proto kernel_ll 
       valid_lft forever preferred_lft forever>
```

## First user-space program

### HOST, in this lab directory: `file build/hello`

```text
<build/hello: ELF 32-bit LSB pie executable, ARM, EABI5 version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-armhf.so.3, BuildID[sha1]=56082b83d1852f2c77fbd0e1898fe8a27a2235ca, for GNU/Linux 3.2.0, not stripped>
```

### BBB: `/home/debian/labs/lab01/hello`

```text
<masha@BeagleBone:~$ /home/masha/labs/lab01/hello
Hello from Lab 01 on BeagleBone Black!>
```

## Shared kernel workspace

### HOST: `ls -lh ~/bbb-workspace/kernel/bb-kernel/deploy`

```text
<masha@DESKTOP-U6MQD9O:~/embedded-linux-course/classroom-templates/lab01-board-bringup$ ls -lh ~/bbb-workspace/kernel/bb-kernel/deploy
total 35M
-rw-r--r-- 1 masha masha 177K Oct  4 12:23 6.12.111-bone73-dtbs.tar.zst
-rw-r--r-- 1 masha masha  26M Oct  4 12:23 6.12.111-bone73-modules.tar.zst
-rwxr-xr-x 1 masha masha 8.4M Oct  4 12:22 6.12.111-bone73.zImage
-rw-r--r-- 1 masha masha 206K Oct  4 12:22 config-6.12.111-bone73>
```

### HOST: `cat ~/bbb-workspace/kernel/bb-kernel/KERNEL/include/config/kernel.release`

```text
<masha@DESKTOP-U6MQD9O:~/embedded-linux-course/classroom-templates/lab01-board-bringup$ cat ~/bbb-workspace/kernel/bb-kernel/KERNEL/include/config/kernel.release
6.12.111-bone73>
```

Do the full HOST and BBB kernel-release strings match exactly?

<No. The BBB is running 6.12.96-bone64, while the kernel workspace contains 6.12.111-bone73.>

Why must Lab 02 use a matching kernel tree?

<Lab 02 needs a matching kernel tree because kernel modules must be built for the same kernel version and configuration as the BBB. Otherwise, the modules may be incompatible.>


Submit this completed report with `src/hello.c` and `Makefile`. Do not commit
images, executables, toolchains, kernel sources, or build artifacts.

