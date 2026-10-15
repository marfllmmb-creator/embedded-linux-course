KDIR = $(HOME)/bbb-workspace/kernel/bb-kernel-6.12.96/KERNEL
ARCH = arm
CROSS_COMPILE = $(HOME)/bbb-workspace/kernel/bb-kernel/dl/gcc-14.4.0-nolibc/arm-linux-gnueabi/bin/arm-linux-gnueabi-

MODULE_NAME = lab02_hello

obj-m += $(MODULE_NAME).o
$(MODULE_NAME)-objs := src/hello.o

.PHONY: all clean

all:
	make -C $(KDIR) M=$(PWD) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) modules

clean:
	make -C $(KDIR) M=$(PWD) clean
