NanoVNA - Very tiny handheld Vector Network Analyzer
==========================================================

[![GitHub release](http://img.shields.io/github/release/ttrftech/NanoVNA.svg?style=flat)][release]
[![CircleCI](https://circleci.com/gh/ttrftech/NanoVNA.svg?style=shield)](https://circleci.com/gh/ttrftech/NanoVNA)

[release]: https://github.com/ttrftech/NanoVNA/releases

<div align="center">
<img src="/doc/nanovna.jpg" width="480px">
</div>

# About

NanoVNA is very tiny handheld Vector Network Analyzer (VNA),designed by edy555, it is a very portable but high-performance vector network analyzer. It is standalone with lcd display, portable device with battery.


Edy555 put his software at https://github.com/ttrftech/NanoVNA
View this link to get the original design documentation for edy555.

You can make or purchase a finished NanoVNA at a low cost. NanoVNA is now the most active vector network analyzer and antenna analyzer project in the community. Usually buying a finished NanoVNA-H is the most convenient way to get NanoVNA.

Edy555 is updating his software, harmonic extensions have been added, usually a well-made NanoVNA can be acquired better than 40dB dynamics at 900MHz . After community discussions, the improved NanoVNA-H can still have 40dB dynamics up to 1.5GHz. Thanks to the excellent performance of the improved NanoVNA-H , edy555 has increased the frequency limit of his 0.7.0 firmware to 2.7GHz, but users should be aware of the uncertainty measured above 1.5GHz.

Cho45 adds TDR (Time Domain Reflectometer) functionality to the NanoVNA. Time domain measurements are widely required by the community to quickly measure the length of the coaxial cable and determine the cable fault point by calculating the discontinuous impedance.

This repository contains source of NanoVNA firmware.

## Prepare ARM Cross Tools

Requires gcc-4.9 to build firmware from source code. (Not work gcc-5.4 or lator, because of SRAM shortage that those runtime use more SRAM)

### MacOSX

Install cross tools and firmware updating tool.

    $ brew tap px4/px4
    $ brew install gcc-arm-none-eabi-49
    $ brew install dfu-util

Otherwise, use toolchains included inside LPCxpresso. Like this.

    $ PATH=$PATH:/Applications/lpcxpresso_7.8.0_426/lpcxpresso/tools/bin

### Linux (ubuntu)

Download arm cross tools from [here](https://launchpad.net/gcc-arm-embedded/4.9/4.9-2015-q3-update).
This version is 32-bit binary, so additional lib32z1 and lib32ncurses5 package required.

    $ wget https://launchpad.net/gcc-arm-embedded/4.9/4.9-2015-q3-update/+download/gcc-arm-none-eabi-4_9-2015q3-20150921-linux.tar.bz2
    $ sudo tar xfj -C /usr/local gcc-arm-none-eabi-4_9-2015q3-20150921-linux.tar.bz2
    $ PATH=/usr/local/gcc-arm-none-eabi-4_9-2015q3/bin:$PATH
    $ sudo apt install -y lib32z1 lib32ncurses5
    $ sudo apt install -y dfu-util

## Fetch source code

Fetch source and submodule.

    $ git clone https://github.com/ttrftech/NanoVNA.git
    $ cd NanoVNA
    $ git submodule update --init --recursive

## Build

Just make in the directory.

    $ make

### Build firmware using docker

You can build firmware using [this docker image](https://cloud.docker.com/u/edy555/repository/docker/edy555/arm-embedded) without installing arm toolchain.

    $ cd NanoVNA
    $ docker run -it --rm -v $(PWD):/work edy555/arm-embedded:4.9 make

## Flash firmware

Boot MCU in DFU mode. To do this, jumper BOOT0 pin at powering device.
Then, burn firmware using dfu-util via USB.

    $ dfu-util -d 0483:df11 -a 0 -s 0x08000000:leave -D build/ch.bin

Or do simply

    $ make flash

## Control from PC

See [python directory](/python/README.md).


## Note

Hardware design material is disclosed to prevent bad quality clone. Please let me know if you would have your own unit.


## Reference

* [Schematics](/doc/nanovna-sch.pdf)
* [PCB Photo](/doc/nanovna-pcb-photo.jpg)
* [Block Diagram](/doc/nanovna-blockdiagram.png)
* Kit available from https://ttrf.tk/kit/nanovna
* Credit: @edy555

[EOF]
