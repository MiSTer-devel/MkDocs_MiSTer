MiSTer uses a combination of various compiled binaries in the finished product. There is a customized minimal Linux Kernel, a bootloader, a Main MiSTer binary that's written in C, and then there are the cores built on the MiSTer framework written in a combination of VHDL, Verilog, and SystemVerilog. In order to compile the "full stack" as it were, you need a variety of tools. I'm writing this guide with the hopes of expanding on it as I explore how to compile the variety of MiSTer cores and programs myself.

## Prerequisites for ARM Cross Compiling

These prerequisites are not completely strict, only some of them are. I'm using a specific linux distro (Ubuntu 20.04.5 LTS in WSL2), but you may find that other distros work for you, however your results may vary. Install the prereqs that I used for the Main MiSTer Binary and Linux kernel compilation this way:

```
sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential git libncurses-dev flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf liblz4-tool bc curl gcc git libssl-dev libncurses5-dev lzop make u-boot-tools libgmp3-dev libmpc-dev
```

Download the correct cross-compiler for compiling ARM binaries on a 64-bit x86-based system:

`wget -c https://developer.arm.com/-/media/Files/downloads/gnu-a/10.2-2020.11/binrel/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz`

Extract this archive to somewhere you prefer, we will use it as a PATH, here we will extract to `/OPT/`:

`tar xf gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz -C /opt`

Add this to your path:

`export PATH=$PATH:/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin`

Optionally set CC:

`export CC='/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin/arm-none-linux-gnueabihf-gcc'`

**Note:** On WSL2 I have to run these export commands again after logging out, this may not be the case in your scenario, there are ways to permanently set them, but I'm preferring not to do that.

## Main MiSTer Binary

The Main MiSTer binary is a good place to start for this guide. I will assume you are either running a linux system or you are using Windows Subsystem for Linux. I'm using Ubuntu current (22.0).

Clone the Main_MiSTer repository:
