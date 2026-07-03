[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)

## Overview

|Platform|Tested|
|---|---|
| UIAPduino Pro Micro CH32V003 V1.4 | &#10004;|

The [UIAPduino Pro Micro CH32V003](https://www.uiap.jp/en/uiapduino/pro-micro/ch32v003/v1dot4) is a tiny RISC-V board (48 MHz, 16KB flash / 2KB SRAM) in the Pro Micro form factor, programmable from the Arduino IDE over a single USB Type-C cable — no external programmer needed.

Note that CH32V003 has only 2KB SRAM, so there is no framebuffer: the image is converted on the host PC into a pre-packed 1bpp array (4000 bytes) stored in flash, and streamed directly into the panel controller RAM over SPI. The sketch draws the picture once at boot, then puts the panel into deep sleep — the image stays on screen while the panel draws only a few µA.

## Hardware Preparison

**IMPORTANT: the board must be reworked to 3.3V before connecting the panel.** The UIAPduino ships at 5V by default (GPIO logic = 5V), which over-drives the 3.3V PIXPAPER panel — the image comes out faint and the 5V logic back-feeds the panel's 3.3V rail. Cut the 5V side of the Volt-Sel solder jumper with a knife (minimal cut — there are traces right above and below it), bridge the 3.3V side with solder, then verify with a multimeter that the 5V side is really open. See the [official board page](https://www.uiap.jp/en/uiapduino/pro-micro/ch32v003/v1dot4) for the jumper location.

Firstly, connecting the PIXPAPER-213-M's connector to the programming cable we've provided. Connect the other end of the cable to the corresponding pins, matching the colors as defined.

<img width="640" alt="image" src="https://github.com/user-attachments/assets/278a84f1-97a0-4ab5-ac1d-c94a1133bda3" />


Then, connect to the UIAPduino specific PINs as follows:

|PIXPAPER-213-M Pinout|UIAPduino Pin assignment (silkscreen)|CH32V003 GPIO|
|---|---|---|
| 3V3 | 3V3 | - |
| GND | GND | - |
| MOSI | 8 | PC6 |
| SCK | 7 | PC5 |
| CS | 6 | PC4 |
| DC | 5 | PC3 |
| RST | 10 | PD0 |
| BUSY | 12 (A3) | PD2 |

## Firmware Update

Step 1. Install the Arduino IDE and the UIAPduino board support

        1. Install Arduino IDE (Windows/Ubuntu both work)
        2. File -> Preferences -> Additional boards manager URLs, add:
           https://github.com/YuukiUmeta-UIAP/board_manager_files/raw/main/package_uiap.jp_index.json
        3. Tools -> Board -> Boards Manager, search "UIAPduino" and install it
        4. Tools -> Board -> select "Pro Micro CH32V003", Board Version "V1.4"

        Note: keep Tools -> Optimize at the default "Smallest (-Os) default".
        Do NOT select the LTO options -- LTO-built firmware does not boot on this board.

Step 2. Prepare the example sketch

        Download the sketch (the .ino must live in a folder with the same name,
        as the Arduino IDE requires):

        $ mkdir pixpaper_213_mono && cd pixpaper_213_mono
        $ wget https://raw.githubusercontent.com/open-ep/arduino-user-space-examples/refs/heads/main/uiap/pixpaper-213-m/quick-update/pixpaper_213_mono.ino
        $ wget https://raw.githubusercontent.com/open-ep/arduino-user-space-examples/refs/heads/main/uiap/pixpaper-213-m/quick-update/img_packed.h

        Then open pixpaper_213_mono.ino in the Arduino IDE.

        The bundled img_packed.h is a ready-to-use sample picture. To display your own
        250x122 PNG, regenerate it with the converter (python3 + opencv required):
        it resizes to 250x122, thresholds at 128 (>=128 -> white) and packs it in the
        panel's native column-major stream order.

        $ sudo apt install python3-opencv
        $ wget https://raw.githubusercontent.com/open-ep/arduino-user-space-examples/refs/heads/main/uiap/pixpaper-213-m/quick-update/png2packed.py
        $ python3 png2packed.py your_image.png -o img_packed.h

Step 3. Enter write standby mode and upload

        While pressing the reset button, connect the board to USB, then immediately
        release the reset button. The board enumerates as an HID device ("32V003").
        After the OS has finished setting up the device, press Upload in the Arduino IDE.
        When the message "Image written." is displayed, writing is complete.

        Note that the sketch has no USB function, so the board disappears from USB once
        it runs -- repeat the reset ritual every time you want to re-flash.
        If the device fails to enumerate (unknown USB device / error -71 in dmesg),
        connect it through a USB 2.0 hub instead of a USB 3.0 port: the bootloader's
        software USB is timing-sensitive and some xHCI hosts cannot enumerate it directly.

        If your wired connection is different with chapter "Hardware Preparison",
        please modify the pin macros at the top of pixpaper_213_mono.ino:

        #define EPD_CS_PIN PC4
        #define EPD_DC_PIN PC3
        #define EPD_RST_PIN PD0
        #define EPD_BUSY_PIN PD2

After boot the panel refreshes once (a full refresh takes about 2 seconds), then the panel enters deep sleep with the image retained.

Expection results: <br>

(photo / video placeholder)

## Contributors

Thanks goes to these wonderful people from open source community:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
        <td align="center" valign="top" width="14.28%"><a href="https://github.com/wigcheng"><img src="https://avatars.githubusercontent.com/u/7148592?v=4" width="100px;" alt="Wig Cheng"/><br /><sub><b>Wig Cheng</b></sub></a><br /><a href="https://github.com/wigcheng/open-ep/commits?author=wigcheng" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

---
