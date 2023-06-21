**BusyBox Overview**

    * Single binary that implements essential Linux programs

    * Symbolic links are used to tell which program is being requested


**Building Busybox**

    * Then sudo make ARCH=arm CROSS_COMPILE=arm-unknown-linux-gnueabi- install

    **Why sudo?**
        - Needed if out rootfs is owned by root  


**Clone the repository and set to default configuration**

    * $ git clone git://busybox.net/busybox.git
    * $ cd busybox
    * $ git checkout 1_26_2 (choose a proper version)
    * $ make distclean
    * $ make defconfig

**Busybox Shared Libraries**

$ aarch64-none-linux-gnu-readelf -a bin/busybox | grep "program interpreter" 

$ aarch64-none-linux-gnu-readelf -a | grep "Shared library"

$ aarch64-none-linux-gnu-gcc -print-sysroot

$ cd $SYSROOT
$ ls -l lib/ld-linux-armhf.so.3


$ cd ~/rootfs
$ cp -a $SYSROOT/lib/ld-linux-armhf.so.3 lib
$ cp -a $SYSROOT/lib/ld-2.22.so lib
$ cp -a $SYSROOT/lib/libc.so.6 lib
$ cp -a $SYSROOT/lib/libc-2.22.so lib
$ cp -a $SYSROOT/lib/libm.so lib
$ cp -a $SYSROOT/lib/libm-2.22.so lib
