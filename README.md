# py32_canbus_dev

KiCad design for a ARM Cortex-M0+ CAN bus development board. The MCU
is a Puya PY32 Series. The board includes a MCP2518 CAN
controller. The specific part is PY032F030K18T6. This can run at a
maximum of 48 MHz, and has 8 kbyte SRAM and 64 kbyte Flash. A USB C
connector provides 5V power only to the development board. The board
must be programmed with a debugger. Design to use a 24 MHz high speed
crystal. There is an onboard LDO that provides 500mA of power at
3.3V. There is an LED and push button connected to 2 of the GPIO
pins. The value of the BOOT0 pin can be set to ground or 3.3V
permanently via the solder bridge. A jumper can be used on the pin
rails in lieue of the solder bridge. All available GPIO pins are
routed to the 2 18pin headers.

## Changes

- Rev A
  Original

## Firmware

Example firmware that blinks the LED. When the user pushbutton is pressed,
the frequency of the LED blink will change.

https://github.com/gpgreen/py32-dev-blink

## Boot configuration

To boot from main flash [0x0800_0000]
  Connect J2-4 to J2-5 (or) solder JP5-1 to center post

To boot from System mem [0x1FFF_0000], or Embedded SRAM [0x2000_0000]
  Connect J2-4 to J2-3 (or) solder JP6-3 to center post

There is an embedded boot loader, programmed in production, in the system memory
block. See the reference manual 3.6.2.

## PIN JUMPER SIGNAL ASSIGNMENT
```
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
        PF3-|8       +-+        8|-GND
        PA0-|9       |O|        9|-GND
        PA1-|10      +-+       10|-PB7
        PA2-|11                11|-PB7
        PA3-|12                12|-PB6
        PA4-|13                13|-PB4
        PA6-|14                14|-PB3
        PA6-|15   UPB          15|-PA15
        PA7-|16   +-+          16|-PA12 [USER LED - GREEN]
        PB0-|17   |O|          17|-PA11 [USER PUSHBUTTON]
        PB1-|18   +-+          18|-PA8
            |                    |
            +--------------------+
```
## Links
- [Puya PY32 Series](https://www.puyasemi.com/cpzx3/info_271_aid_247_kid_246.html)
- [Software template for PY32 Series by Jay Carlson](https://github.com/jaydcarlson/py32-template)
- [Fork of template for these boards](https://github.com/gpgreen/py32-dev-blink)
- [Tech documentation for py32f030](https://www.puyasemi.com/uploadfiles/2022/11/PY-MCU%E8%B5%84%E6%96%99-20221117.rar)
