# 4190.307 Operating Systems (Spring 2020)
# Installing xv6-riscv

## Installation Overview

The installation of ``xv6`` requires the following steps:

* __GNU RISC-V toolchain__: You require 64-bit GNU RISC-V toolchain to compile the ``xv6`` source code. 
* __QEMU for emulating a multic-core RISC-V machine__: In order to run ``xv6`` on a machine with the x86 processor, you need to install the open source machine emulator called [QEMU](https://www.qemu.org).
* __xv6__: You need to build the kernel and the root file system image from the ``xv6`` source code.

We provide the detailed instructions below on how to run ``xv6`` on Ubuntu, macOS, and Windows.

## Installing xv6 on Ubuntu

The following instructions are based on the latest stable Ubuntu version 18.04.4 LTS.

* Install the prerequite packages

```
$ sudo apt install git build-essential
```

* You need the GCC version 8 or higher, but the default GCC package, ``gcc-riscv64-linux-gnu``, in Ubuntu 18.04.4 LTS contains the GCC version 7.4.0. Instead, install the GCC version 8.3.0 as follows and link it as ``riscv64-linux-gnu-gcc``. Your 64-bit GNU toolchain will be installed in the ``/usr/bin`` directory.

```
$ sudo apt install gcc-8-riscv64-linux-gnu binutils-riscv64-linux-gnu
$ cd /usr/bin
$ sudo ln -s riscv64-linux-gnu-gcc-8 riscv64-linux-gnu-gcc
```

* Currently, no QEMU package is available in Ubuntu for the RISC-V processor. Therefore, you have to build it manually as follows. The QEMU version should be 4.1.0 or higher. You need to install ``libglib2.0-dev`` and ``libpixman-1-dev`` packages as well because they are required to compile QEMU. 

```
$ sudo apt install libglib2.0-dev libpixman-1-dev
$ cd ~
$ wget https://download.qemu.org/qemu-4.1.0.tar.xz
$ tar xf qemu-4.1.0.tar.xz
$ cd qemu-4.1.0
$ ./configure --disable-kvm --disable-werror --prefix=/usr/local --target-list="riscv64-softmmu"
$ make
$ sudo make install
```

The final executable file ``qemu-system-riscv64`` will be installed in the ``/usr/local/bin`` directory. Perform the following command so that the directory is appended to your ``PATH`` environment variable.

```
$ echo "PATH=/usr/local/bin:\$PATH" >> ~/.bashrc
$ source ~/.bashrc
```

Check your installation by running the following command.

```
$ qemu-system-riscv64 --version
QEMU emulator version 4.1.0
Copyright (c) 2003-2019 Fabrice Bellard and the QEMU Project developers
```

* Now you are ready to install ``xv6``. Please take the following steps.

```
$ cd ~
$ git clone https://github.com/snu-csl/xv6-riscv
$ cd xv6-riscv
$ make 
```

* You can run ``xv6`` using the ``make qemu`` command. The output should look like this. 

```
$ make qemu
qemu-system-riscv64 -machine virt -bios none -kernel kernel/kernel -m 3G -smp 3 -nographic -drive file=fs.img,if=none,format=raw,id=x0 -device virtio-blk-device,drive=x0,bus=virtio-mmio-bus.0

xv6 kernel is booting

hart 2 starting
hart 1 starting
init: starting sh
$
```

To terminate QEMU, please press ``ctrl-a`` and then ``x`` in your keyboard.


## Installing xv6 on macOS

The following instructions are based on the latest macOS Catalina 10.15.3.

* If your Mac does not have xcode command line tools, install them using the following command.

```
% xcode-select --install
```

* If your Mac does not have ``homebrew``, a package manager for macOS, install it as follows.

```
% /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

* Now install the 64-bit RISC-V GNU toolchain using the ``brew`` command.

```
% brew tap riscv/riscv
% brew install riscv-tools
```

In case you encounter some error messages such as ``"Cannot tap riscv/riscv: invalid syntax in tap!"``, try the following command instead (it may take a while).
```
% brew tap riscv/riscv https://github.com/n-wen/homebrew-riscv
% brew install riscv-tools
```

When successful, GNU RISC-V toolchain is installed in the ``/usr/local/opt/riscv-gnu-toolchain/bin`` directory. Perform the following command to add the directory in your PATH environment variable.

``` 
% echo "PATH=/usr/local/opt/riscv-gnu-toolchain/bin:\$PATH" >> ~/.bash_profile (or ~/.zshrc)
% source ~/.bash_profile (or ~/.zshrc)
```

* Install QEMU using the ``brew`` utility

``` 
% brew install qemu
```

* Download ``xv6``
```
% cd ~
% git clone https://github.com/snu-csl/xv6-riscv
% cd xv6-riscv
```

* To compile xv6 on macOS, you have to modify the ``Makefile`` slightly. Locate the line with "``#TOOLPREFIX =``" (line 212) in ``Makefile`` and modify it to represent the prefix of your toolchain. Also, you need to define ``CPPFLAGS`` as null as shown below.

```
(Modify xv6 Makefile line 212)
...
TOOLPREFIX = /usr/local/opt/riscv-gnu-toolchain/bin/riscv64-unknown-elf-
CPPFLAGS = 
...
```

* Build and run ``xv6``
```
% make
% make qemu
```


## Installing xv6 on Windows 10

The easiest way of running ``xv6`` on Windows is to turn on the "Windows Subsystem for Linux (WSL)" and then install Ubuntu from the Microsoft Store. For detailed instructions, please refer to [this page](https://docs.microsoft.com/ko-kr/windows/wsl/install-win10).

The latest Ubuntu version in the Microsoft Store is 18.04 LTS. Once you have installed Ubuntu 18.04 LTS, perform the following commands to upgrade your Ubuntu version to 18.04.4 LTS. 

```
$ sudo apt update
$ sudo apt upgrade
```

And then just follow the above instructions for [installing xv6 on Ubuntu](#installing-xv6-on-ubuntu).



Have fun!

[Jin-Soo Kim](mailto:jinsoo.kim_AT_snu.ac.kr)  
[Systems Software and Architecture Laboratory](http://csl.snu.ac.kr)  
[Dept. of Computer Science and Engineering](http://cse.snu.ac.kr)  
[Seoul National University](http://www.snu.ac.kr)
