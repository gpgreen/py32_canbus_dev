# py32_canbus_dev

KiCad design for a ARM Cortex-M0+ CAN bus development board. The MCU
is a Puya PY32 Series. The board includes a MCP2518 CAN
controller. The specific part is PY032F030K18T6. This can run at a
maximum of 48 MHz, and has 8 kbyte SRAM and 64 kbyte Flash. A USB B
mini connector provides 5V power and interfaces with a FTDI device
wired as a Serial Comm to the development board. The board must be
programmed with a debugger, ie at this time it cannot be programmed
over the usb. Design use's a 24 MHz high speed crystal. There is an
onboard LDO that provides 500mA of power at 3.3V. There is an LED
connected to 1 of the GPIO pins. The value of the BOOT0 pin can be set
to ground or 3.3V permanently via the solder bridge. A jumper can be
used on the pin rails in lieue of the solder bridge. All available
GPIO pins are routed to the 2 18pin headers.

## Changes

- Rev A
  Original

## Firmware

Example firmware that blinks the LED. When the user pushbutton is pressed,
the frequency of the LED blink will change.

https://github.com/gpgreen/py32-dev-blink

## Boot configuration

A boot configuration must be selected for the development board to
operate. If a program has been flashed then booting from main flash
should be selected for that program to run.

To boot from main flash [0x0800_0000] Connect J2-4 to J2-5 (or) solder
  JP5-1 to center post

To boot from System mem [0x1FFF_0000], or Embedded SRAM [0x2000_0000]
  Connect J2-4 to J2-3 (or) solder JP6-3 to center post

There is an embedded boot loader, programmed during mcu chip production, in the system memory
block. See the reference manual 3.6.2.

## PIN JUMPER SIGNAL ASSIGNMENT
```
                     USB-B
                    +-----+
            +--------------------+
            |J3     |     |    J2|
        VDD-|1      +-----+     1|-GND
        GND-|2                  2|-GND
       +3.3-|3                  3|-+3.3
[RESET] PF2-|4                  4|-PF4 [BOOT0_PRE]
[SWCLK]PA14-|5                  5|-GND
[SWDIO]PA13-|6                  6|-GND
        GND-|7       RST        7|-GND
        PF3-|8       +-+        8|-PB7 [USB RX]
        PA0-|9       |O|        9|-PB6 [USB TX]
  [SCK] PA1-|10      +-+       10|-PB5
 [MOSI] PA2-|11                11|-PB4
        PA3-|12                12|-PB3
  [NSS] PA4-|13                13|-PA15
[CAN I] PA5-|14                14|-PA12 [USER LED - GREEN]
 [MISO] PA6-|15                15|-PA11
        PA7-|16                16|-PA10
        PB0-|17                17|-PA9
        PB1-|18    +------+    18|-PA8
            |     1| o  o |2     |
            +--------------------+
                     H  L
                     CAN
```
## Links
- [Puya PY32 Series](https://www.puyasemi.com/cpzx3/info_271_aid_247_kid_246.html)
- [Software template for PY32 Series by Jay Carlson](https://github.com/jaydcarlson/py32-template)
- [Fork of template for these boards](https://github.com/gpgreen/py32-dev-blink)
- [Firmware library for py32f030](https://www.puyasemi.com/download_path/%E5%BA%93%E5%87%BD%E6%95%B0%E4%B8%8E%E4%BE%8B%E7%A8%8B/MCU/PY32F0xx_Firmware_V1.4.1.zip)
