[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

## Hardware Preparison

[Milk-V Duo256M](https://milkv.io/duo) is an ultra-compact RISC-V embedded Linux platform based on the SOPHGO SG2002 SoC. It exposes a 26-PIN header (the same footprint as a Raspberry Pi Pico), and one of its SPI masters (SPI2) is routed to that header, so it can drive the panel without any extra hardware.

Firstly, connecting the PIXPAPER-213-M's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

<img width="640" alt="image" src="https://github.com/user-attachments/assets/278a84f1-97a0-4ab5-ac1d-c94a1133bda3" />

Then, connect to the Milk-V Duo256M specific PINs of 26-PIN header as follows:

| PIXPAPER-213-M | Duo256M PIN | Name | Function |
|:---|:---|:---|:---|
| 3.3V | 36 | 3V3(OUT) | 3.3V power output |
| GND | 3 | GND | Ground (pin 8 / 13 / 18 / 23 also work) |
| SCK | 9 | GP6 | SPI2_SCK |
| MOSI | 10 | GP7 | SPI2_SDO |
| CS# | 12 | GP9 | SPI2_CS |
| DC# | 21 | GP16 | XGPIOA[23], `gpiochip0` line 23 |
| RST# | 22 | GP17 | XGPIOA[24], `gpiochip0` line 24 |
| BUSY | 24 | GP18 | XGPIOA[22], `gpiochip0` line 22 |

> **Note:** DC#, RST# and BUSY are plain GPIOs, so any free pin works. GP16 / GP17 / GP18 are picked because they default to GPIO in the Milk-V pinmux, are not claimed by any device tree node, and all three live on the same GPIO chip (`gpiochip0` = XGPIOA), which keeps the source simple. GP26 / GP27 are **not** usable here: their logic level is 1.8V.

## Driver Installation instructions

|Kernel|Tested|
|---|---|
| 5.10.4 |&#10004;|

Because there has a SPI interface on Linux already, so no need any tweaking in kernel space, just need to checking the device node is exist or not <br>

    ls /dev/spidev0.0

## User-Space Utility instructions (Linux OS)

Step 1. Install necessary packages

        The Duo256M rootfs is built by Buildroot inside duo-buildroot-sdk-v2, so the SPI and GPIO
        user-space packages are selected at build time instead of being installed on the target.
        None of the three below are enabled in the stock board defconfig, so all of them have to
        be added by hand to buildroot/configs/milkv-duo256m-musl-riscv64-sd_defconfig:

        BR2_PACKAGE_PYTHON_SPIDEV=y
        BR2_PACKAGE_LIBGPIOD=y
        BR2_PACKAGE_LIBGPIOD_TOOLS=y

        Then rebuild the image:
        $ ./build.sh milkv-duo256m-musl-riscv64-sd

Step 2. Prepare a 250x122 size picture what you want to showing, then make a image raw data based header file

        Download the PNG to RAW converter base on python3, remember to install opencv package first
        $ sudo apt install python3-opencv
        $ wget https://github.com/open-ep/linux-user-space-examples/raw/refs/heads/master/2.13/mono/spi/png2bit.py

        Download the sample image
        $ wget https://github.com/open-ep/linux-user-space-examples/raw/refs/heads/master/2.13/mono/spi/test.png

        Then, rename your PNG file as test.png, and excute the python script
        $ python3 png2bit.py test.png

        It will generate a output file: png_HEX.h, the copy the same folder with pixpaper-213-m-test-milkv-duo256m.c.
        Note that this step must be running on the host PC side for the Duo256M, because the target
        rootfs has no compiler; png_HEX.h must be put into the folder with c file together before
        compiling.

Step 3. The Duo256M rootfs ships without a native toolchain, so the utility is cross-compiled on the host with the SDK toolchain and then copied to the board.

        On the host PC, inside duo-buildroot-sdk-v2:

        PIXPAPER-213-M:
        TODO: publish pixpaper-213-m-test-milkv-duo256m.c to linux-user-space-examples. Until then,
        take it from this repository. The sources already in that repo are samples written for
        other boards, so their EPD_SPI_DEVICE / EPD_GPIO_CHIP / DC# / RST# / BUSY macros point at
        that board's pinout, never at the Duo256M one, and must be set as shown below.

        $ SDK=$(pwd)
        $ SYSROOT=$SDK/buildroot/output/milkv-duo256m-musl-riscv64-sd/host/riscv64-buildroot-linux-musl/sysroot
        $ $SDK/host-tools/gcc/riscv64-linux-musl-x86_64/bin/riscv64-unknown-linux-musl-gcc \
                -O2 -Wall --sysroot=$SYSROOT -o epd_test pixpaper-213-m-test-milkv-duo256m.c -lgpiod

        Copy the binary to the board (SD card, scp over USB-NCM, ...) and run it there:

        # ./epd_test            # full mono refresh
        # ./epd_test fast       # fast mono refresh
        # ./epd_test gray4      # 4-grayscale refresh
        # ./epd_test partial    # partial-update demo, two images swapping
        # ./epd_test clock      # HH:MM:SS clock, one partial update per second

        Note that if your wired connection is different with chapter 1 "Hardware Preparison", especially DC# PIN, RST# PIN, and BUSY PIN, also can issue command 'gpioinfo' to check the gpio pin detail.
        Please modify the specific macros definition of pixpaper-213-m-test-milkv-duo256m.c:

        #define EPD_SPI_DEVICE "/dev/spidev0.0"
        #define EPD_GPIO_CHIP "gpiochip0"
        #define EPD_DC_PIN 23
        #define EPD_RST_PIN 24
        #define EPD_BUSY_PIN 22

Expection results: <br>
Coming soon

## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
        <td align="center" valign="top" width="14.28%"><a href="https://github.com/seanwascoding"><img src="https://github.com/seanwascoding.png" width="100px;" alt="Sean Chang"/><br /><sub><b>Sean Chang</b></sub></a><br /><a href="https://github.com/open-ep/PIXPAPER-213-M/commits?author=seanwascoding" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
