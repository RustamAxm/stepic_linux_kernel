obj-m += hello_w.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean

load:
	sudo insmod hello_w.ko
	sudo dmesg -c
unload:
	sudo rmmod hello_w.ko
	sudo dmesg -c
