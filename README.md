# About
This is a source code of Linux Kernel 3.14 for OpenRex board.

### About OpenRex
OpenRex is an open source hardware and software project.


Website: http://www.imx6rex.com/open-rex/

### More detailed software & hardware manual
For more detailed instructions about how to prepare software for OpenRex, go to:


http://www.imx6rex.com/open-rex/software/how-develop-your-own-software-uboot-linux-filesystem-yocto/

# Download source code
    git clone -b jethro https://github.com/FEDEVEL/openrex-linux-3.14.git
    cd openrex-linux-3.14

# Install & select cross compiler

### If you do not have any compiler installed (or you are not sure)
    apt-get install gcc-arm-linux-gnueabihf
    export CROSS_COMPILE=arm-linux-gnueabihf-

### If you have a compiler installed
    export CROSS_COMPILE=/opt/freescale/usr/local/gcc-4.6.2-glibc-2.13-linaro-multilib-2011.12/fsl-linaro-toolchain/bin/arm-none-linux-gnueabi-

# Setup Architecture
    export ARCH=arm

# Build 
Here are instructions how to compile the source code

### QUAD
    make clean
    make imx_v7_defconfig
    make -j4 zImage imx6q-openrex.dtb
    cp arch/arm/boot/zImage /tftp/imx6/zImage-imx6q-openrex
    cp arch/arm/boot/dts/imx6q-openrex.dtb /tftp/imx6/imx6q-openrex.dtb

### SOLO
    make clean
    make imx_v7_defconfig
    make -j4 zImage imx6s-openrex.dtb
    cp arch/arm/boot/zImage /tftp/imx6/zImage-imx6s-openrex
    cp arch/arm/boot/dts/imx6s-openrex.dtb /tftp/imx6/imx6s-openrex.dtb

# Update OpenRex SD card with Linux
Go to OpenRex board, interrupt uBoot booting process (press any key). Then write following commands:


    run update_kernel;run update_fdt;reset


Note: if you would like to test the kernel without saving it to SD card, go to uBoot and use following commands:


    tftp 0x12000000 imx6/zImage-imx6q-openrex; tftp 0x18000000 imx6/imx6q-openrex.dtb;bootz 0x12000000 - 0x18000000

# Appendix
Here is a list of files, where we usually do changes:


    arch/arm/boot/dts/imx6q-openrex.dts
    arch/arm/boot/dts/imx6s-openrex.dts
    arch/arm/boot/dts/imx6qdl-openrex.dtsi
    


