MiSTer uses a combination of various compiled binaries in the finished product. There is a customized minimal Linux Kernel, a bootloader, a Main MiSTer binary that's written in C, and then there are the cores built on the MiSTer framework written in a combination of VHDL, Verilog, and SystemVerilog. In order to compile the "full stack" as it were, you need a variety of tools.

## To compile MiSTer FPGA cores

The vast majority of MiSTer FPGA cores currently use Quartus 17.0.2 for compilation. Here are the download links for both Windows and Linux:

| Download URL                                                                                                                           | SHA1 Checksum                              |
|----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| [Linux](https://download.altera.com/akdlm/software/acdsinst/17.0std.2/602/ib_tar/Quartus-lite-17.0.2.602-linux.tar){target=_blank}     | `02aebab728d54e3ca8660d2646fdf93bc669b0ac` |
| [Windows](https://download.altera.com/akdlm/software/acdsinst/17.0std.2/602/ib_tar/Quartus-lite-17.0.2.602-windows.tar){target=_blank} | `01d1f9cea037cf4b8c666da1193f94ba626b6fb3` |

The Linux version is intended to work with Ubuntu 18.xx, you may have to adjust by downloading some missing dependencies if you use a newer version or another distribution.

Open the .qpf file from the MiSTer core you wish to compile with Quartus and press the play button. It's as simple as that!

## General prerequisites for ARM Cross Compiling

These prerequisites are not completely strict, only some of them are. I'm using a specific linux distro (Ubuntu 20.04.5 LTS in WSL2), but you may find that other distros work for you, however your results may vary. Install the prereqs that I use for the Main MiSTer Binary and Linux kernel compilation this way:

```sh
sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential git libncurses-dev flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf liblz4-tool bc curl gcc git libssl-dev libncurses5-dev lzop make u-boot-tools libgmp3-dev libmpc-dev
```

Download the correct cross-compiler for compiling ARM binaries on a 64-bit x86-based system:

```sh
wget -c https://developer.arm.com/-/media/Files/downloads/gnu-a/10.2-2020.11/binrel/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz
```

Extract this archive to somewhere you prefer, we will use it as a PATH, so here we will extract to `/opt`:

```sh
tar xf gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf.tar.xz -C /opt
```

Add this to your path temporarily each time you compile:

```sh
export PATH=/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin:$PATH
```

**Note:** On WSL2 I have to run these export commands again after logging out, this may not be the case in your scenario, there are ways to permanently set them, but I'm preferring not to do that, you can also use them as parameters with `make` like normal (e.g. `PATH=/opt/gcc-arm-10.2-2020.11-x86_64-arm-none-linux-gnueabihf/bin:$PATH make -j30`).

## Main MiSTer Binary

The Main MiSTer binary is a good place to start for this guide. 

### Linux (including WSL)

Clone the Main_MiSTer repository:

```sh
git clone https://github.com/MiSTer-devel/Main_MiSTer.git
```

Then `cd` into that directory that was created and follow up with `make`.

### macOS

With Apple Silicon, the commonly used toolchains do not run directly as they are built for x86_64.

You can take advantage of an [IDE with devcontainers support](https://containers.dev/supporting){target=_blank} as the Main MiSTer repo includes a [devcontainer configuration](https://github.com/MiSTer-devel/Main_MiSTer/tree/master/.devcontainer){target=_blank}.

Make sure you have enough RAM available or you will experience [disconnects](https://code.visualstudio.com/docs/remote/troubleshooting#_troubleshooting-hanging-or-failing-connections){target=_blank}. E.g. if using [Colima](https://github.com/abiosoft/colima){target=_blank}, the following appears sufficient to quickly compile MiSTer: 
```
colima start --cpu 4 --memory 8
```

## MiSTer Linux Kernel

Edit your sources file:

```sh
sudo nano /etc/apt/sources.list
```

Uncomment all of the lines which start with `deb-src` and then run the following:

```sh
sudo apt-get update
sudo apt-get build-dep linux
```

to be continued... If you would like to contribute to this article, please do! :)
