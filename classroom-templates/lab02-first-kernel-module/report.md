# Lab 02 report

- Student name: Maria Bogdanova
- GitHub username: marfllmmb

Replace each placeholder with your own command output. Run HOST build commands
from this lab directory and BBB module commands from `/home/debian/labs/lab02`.
Keep the complete `vermagic`, not only its release prefix.

## Prerequisites and module metadata

### BBB: `uname -r`

```text
<6.12.96-bone64>
```

### HOST: `cat ~/bbb-workspace/kernel/bb-kernel/KERNEL/include/config/kernel.release`

```text
<masha@DESKTOP-U6MQD9O:~/embedded-linux-course$ cat ~/bbb-workspace/kernel/bb-kernel-6.12.96/KERNEL/include/config/kernel.release
6.12.96-bone64>
```

### HOST: `file lab02_hello.ko`

```text
<masha@DESKTOP-U6MQD9O:~/embedded-linux-course$ cd ~/embedded-linux-course/classroom-templates/lab02-first-kernel-module
file lab02_hello.ko
lab02_hello.ko: ELF 32-bit LSB relocatable, ARM, EABI5 version 1 (SYSV), BuildID[sha1]=7c62b42bce61783350cda64c0e1d2705aac796c6, not stripped
masha@DESKTOP-U6MQD9O:~/embedded-linux-course/classroom-templates/lab02-first-kernel-module$ file lab02_hello.ko
lab02_hello.ko: ELF 32-bit LSB relocatable, ARM, EABI5 version 1 (SYSV), BuildID[sha1]=7c62b42bce61783350cda64c0e1d2705aac796c6, not stripped
masha@DESKTOP-U6MQD9O:~/embedded-linux-course/classroom-templates/lab02-first-kernel-module$ >
```

### HOST: `modinfo lab02_hello.ko | grep vermagic`

```text
<masha@DESKTOP-U6MQD9O:~/embedded-linux-course/classroom-templates/lab02-first-kernel-module$ modinfo lab02_hello.ko | grep vermagic
vermagic:       6.12.96-bone64 preempt mod_unload ARMv7 thumb2 p2v8>
```

Explain why the full kernel releases must match and whether yours match:

<The full kernel releases must match because the module is compiled for a specific kernel version and configuration. If they differ, the module may fail to load due to incompatible symbols or vermagic.The full kernel releases did not match at first because I was using the wrong kernel build tree (6.12.111-bone73). After switching to the correct tree, both the BeagleBone Black kernel and the build tree reported 6.12.96-bone64. The module’s vermagic also matches 6.12.96-bone64, so they now match.>

## Load, inspect, and unload on BBB

### `sudo insmod ./lab02_hello.ko name=Student` and `sudo dmesg | tail -20`

```text
<sudo insmod ./lab02_hello.ko name=Student
[sudo] password for masha: 
masha@BeagleBone:~$ sudo dmesg | tail -20
[   34.481944] at24 0-0050: 4096 byte 24c32 EEPROM, writable, 1 bytes/write
[   37.576994] configfs-gadget.g_multi gadget.0: HOST MAC 78:04:73:41:12:67
[   37.607541] configfs-gadget.g_multi gadget.0: MAC 78:04:73:41:12:68
[   46.637074] remoteproc remoteproc1: 4a334000.pru is available
[   46.667678] remoteproc remoteproc2: 4a338000.pru is available
[   82.253007] systemd-journald[225]: File /var/log/journal/edb7b37b49c449afba2eb4c28b706958/user-1000.journal corrupted or uncleanly shut down, renaming and replacing.
[ 4368.953622] lab02_hello: loading out-of-tree module taints kernel.
[ 4368.960552] hello_module: Hello, Maria, from kernel space on BBB!
[ 4388.730568] hello_module: Goodbye from kernel space on BBB!
[ 5371.516290] hello_module: Hello, Maria, from kernel space on BBB!
[ 5383.496603] hello_module: Goodbye from kernel space on BBB!
[ 5388.445944] hello_module: Hello, Maria, from kernel space on BBB!
[ 5414.823540] hello_module: Goodbye from kernel space on BBB!
[ 5476.405769] hello_module: Hello, Maria, from kernel space on BBB!
[ 5493.675474] hello_module: Goodbye from kernel space on BBB!
[ 5742.841307] hello_module: Hello, Maria, from kernel space on BBB!
[ 5742.848434] hello_module: Hello, Maria, from kernel space on BBB!
[ 5742.855922] hello_module: Hello, Maria, from kernel space on BBB!
[ 5767.420441] hello_module: Goodbye from kernel space on BBB!
[ 6944.838435] hello_module: Hello, Student, from kernel space on BBB!
masha@BeagleBone:~$ >
```

### `lsmod | grep lab02_hello`

```text
<masha@BeagleBone:~$ lsmod | grep lab02_hello
lab02_hello            12288  0
masha@BeagleBone:~$ >
```

### `sudo rmmod lab02_hello` and `sudo dmesg | tail -20`

```text
<masha@BeagleBone:~$ sudo rmmod lab02_hello
masha@BeagleBone:~$ sudo dmesg | tail -20
[   37.576994] configfs-gadget.g_multi gadget.0: HOST MAC 78:04:73:41:12:67
[   37.607541] configfs-gadget.g_multi gadget.0: MAC 78:04:73:41:12:68
[   46.637074] remoteproc remoteproc1: 4a334000.pru is available
[   46.667678] remoteproc remoteproc2: 4a338000.pru is available
[   82.253007] systemd-journald[225]: File /var/log/journal/edb7b37b49c449afba2eb4c28b706958/user-1000.journal corrupted or uncleanly shut down, renaming and replacing.
[ 4368.953622] lab02_hello: loading out-of-tree module taints kernel.
[ 4368.960552] hello_module: Hello, Maria, from kernel space on BBB!
[ 4388.730568] hello_module: Goodbye from kernel space on BBB!
[ 5371.516290] hello_module: Hello, Maria, from kernel space on BBB!
[ 5383.496603] hello_module: Goodbye from kernel space on BBB!
[ 5388.445944] hello_module: Hello, Maria, from kernel space on BBB!
[ 5414.823540] hello_module: Goodbye from kernel space on BBB!
[ 5476.405769] hello_module: Hello, Maria, from kernel space on BBB!
[ 5493.675474] hello_module: Goodbye from kernel space on BBB!
[ 5742.841307] hello_module: Hello, Maria, from kernel space on BBB!
[ 5742.848434] hello_module: Hello, Maria, from kernel space on BBB!
[ 5742.855922] hello_module: Hello, Maria, from kernel space on BBB!
[ 5767.420441] hello_module: Goodbye from kernel space on BBB!
[ 6944.838435] hello_module: Hello, Student, from kernel space on BBB!
[ 7067.111546] hello_module: Goodbye from kernel space on BBB!
masha@BeagleBone:~$ >
```

## Parameter tests on BBB

After implementing the student tasks, rebuild, check metadata, and copy the
module again. Unload after every successful load before testing another case.
For each case record the command, result, and relevant `dmesg` output. Capture
`echo $?` immediately after `insmod` to record its exit status.

### Valid name: `name=YourName`

```text
<sudo insmod ./lab02_hello.ko name=YourName
echo $?
sudo dmesg | tail -n 5
sudo rmmod lab02_hello
0
[ 7234.222285] hello_module: Hello, Maria, from kernel space on BBB!
[ 7234.228598] hello_module: Hello, Maria, from kernel space on BBB!
[ 7234.237035] hello_module: Hello, Maria, from kernel space on BBB!
[ 7234.648056] hello_module: Goodbye from kernel space on BBB!
[ 7320.639328] hello_module: Hello, YourName, from kernel space on BBB!
masha@BeagleBone:~$ >
```

### Invalid empty name: `name=` (must return `-EINVAL`)

```text
< sudo insmod ./lab02_hello.ko name=""
echo $?
sudo dmesg | tail -n 5
insmod: ERROR: could not insert module ./lab02_hello.ko: Invalid parameters
1
[ 7234.228598] hello_module: Hello, Maria, from kernel space on BBB!
[ 7234.237035] hello_module: Hello, Maria, from kernel space on BBB!
[ 7234.648056] hello_module: Goodbye from kernel space on BBB!
[ 7320.639328] hello_module: Hello, YourName, from kernel space on BBB!
[ 7321.052995] hello_module: Goodbye from kernel space on BBB!
masha@BeagleBone:~$ >
```

### Valid count: test `count=1` and `count=10`

```text
<masha@BeagleBone:~$ sudo insmod ./lab02_hello.ko name=Maria count=1
echo $?
sudo dmesg | tail -n 5
0
[ 7504.962157] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.968760] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.976078] hello_module: Hello, Maria, from kernel space on BBB!
[ 7505.385535] hello_module: Goodbye from kernel space on BBB!
[ 8029.999993] hello_module: Hello, Maria, from kernel space on BBB!



masha@BeagleBone:~$ sudo insmod ./lab02_hello.ko name=Maria count=10
echo $?
sudo dmesg | tail -n 15
sudo rmmod lab02_hello
0
[ 7234.648056] hello_module: Goodbye from kernel space on BBB!
[ 7320.639328] hello_module: Hello, YourName, from kernel space on BBB!
[ 7321.052995] hello_module: Goodbye from kernel space on BBB!
[ 7455.944250] hello_module: Hello, Maria, from kernel space on BBB!
[ 7480.083539] hello_module: Goodbye from kernel space on BBB!
[ 7504.911999] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.919217] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.926913] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.933632] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.941108] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.947956] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.955341] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.962157] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.968760] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.976078] hello_module: Hello, Maria, from kernel space on BBB!
masha@BeagleBone:~$ 
>
```

### Invalid count: test `count=0` and `count=11` (must return `-EINVAL`)

```text
<masha@BeagleBone:~$ sudo insmod ./lab02_hello.ko name=Maria count=0
echo $?
sudo dmesg | tail -n 5
insmod: ERROR: could not insert module ./lab02_hello.ko: Invalid parameters
1
[ 7504.955341] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.962157] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.968760] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.976078] hello_module: Hello, Maria, from kernel space on BBB!
[ 7505.385535] hello_module: Goodbye from kernel space on BBB!
masha@BeagleBone:~$ 



masha@BeagleBone:~$ sudo insmod ./lab02_hello.ko name=Maria count=11
echo $?
sudo dmesg | tail -n 5
insmod: ERROR: could not insert module ./lab02_hello.ko: Invalid parameters
1
[ 7504.955341] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.962157] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.968760] hello_module: Hello, Maria, from kernel space on BBB!
[ 7504.976078] hello_module: Hello, Maria, from kernel space on BBB!
[ 7505.385535] hello_module: Goodbye from kernel space on BBB!
masha@BeagleBone:~$ >
```

## Questions

1. Why does a kernel module not have `main()`?

   <A kernel module runs inside the Linux kernel and uses initialization and cleanup functions instead of main().>

2. What does `module_init()` do?

   <module_init() specifies the function that runs when the module is loaded.>

3. What does `vermagic` show?

   <vermagic shows the kernel version and compatibility information for which the module was built>

4. Why can `insmod` fail with `invalid module format`?

   <It can fail if the module was built for an incompatible kernel version, architecture, or configuration.>

5. What does the `name` parameter do, and what do its permissions `0444` mean?

   <The name parameter specifies the name printed in the greeting message. Permissions 0444 mean that the parameter is readable by everyone but cannot be changed through the module parameter interface at runtime.>


Submit `src/hello.c`, `Makefile`, and this completed `report.md`. Do not commit
`.ko`, `.o`, `.mod`, `.mod.c`, `.cmd`, `Module.symvers`, or `modules.order`.
