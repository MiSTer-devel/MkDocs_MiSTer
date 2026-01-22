---
hide:
  - toc
---


A MiSTer stack consists of the DE10-Nano board from Terasic, coupled with a number of [add-on boards](../basics/addons.md).

## Pre-built solutions and clones

Over time, two kinds of hardware solutions have appeared in the market:

- pre-built kits (using the DE10-Nano)
- clones of the DE10-Nano[^1] (and their equivalent pre-built kits)

We don't cover the various options here and their trade-offs. MiSTer is designed and tested with the DE10-Nano board and the stack we describe below. 

[^1]: Hardware solutions using clone boards can aim for compatibility with the MiSTer project, but with minor differences in hardware, ocasional incompatibilities can occur (although they can also be fixed, it's not within the scope of the project). We refer to the respective sellers for compatibility and support.

## Build from scratch

There are a few things you will need in order to setup your MiSTer:

* Terasic DE10-Nano
* MicroSD card (minimum 4GB) and MicroSD Card Reader
* USB OTG Adapter or a [MiSTer USB Hub Add-On Board](../basics/addons.md#usb-hub-addon-board){target=_blank} (no USB devices will work without this)
* USB Keyboard
* HDMI Display and HDMI Cable

Recommended:

* [MiSTer SDRAM Add-On Board](../basics/addons.md#128mb-sdram-addon-board){target=_blank} (optional but many cores require it)
* USB Gamepad
* Cooling for the FPGA
* Internet connection

### Where to buy
**DE10-Nano:**

* [Terasic](http://de10-nano.terasic.com){target=_blank}
* [Digikey](https://www.digikey.com/en/products/detail/terasic-inc/P0496/6817231){target=_blank}
* [Mouser](https://www.mouser.com/ProductDetail/Terasic-Technologies/P0496?qs=sGAEpiMZZMug%252BNZZT2EIMybLXjFfYtXHeZj9cpOi%2FsY%3D){target=_blank}

**SDRAM:**

The MiSTer SDRAM add-on board is required by many cores, like the SNES, NES, Playstation, and Game Boy cores. There are multiple sellers out there which sell these, and you can also assemble it yourself if you are skilled at soldering.

**USB OTG Adapter/Hub:**

Preferably, the MiSTer USB Hub Add-on board which you can assemble yourself if you are good at soldering, or you can [buy from the various shops that sell them](../basics/addons.md#where-to-buy){target=_blank} instead.

At a minimum, the [MakerSpot Micro USB OTG Hub](https://www.amazon.com/MakerSpot-Accessories-Charging-Extension-Raspberry/dp/B01JL837X8){target=_blank} works very well for the MiSTer, if you are looking for a very cheap option.

**Cooling:**

The processor on the DE10-Nano is 21.5mm x 21.5mm so a heatsink that is around this size is suitable. If using one larger than these dimensions, please make sure to to not let the heatsink touch other electronic components outside the processor.

There is no mounting mechanism for the heatsink, you will need to use an "adhesive thermal pad". 3M makes some good ones, and the heatsinks you can buy in this size usually come with these kinds of thermal pads already.

Do not apply a lot of pressure and do not touch the components directly with your fingers, as static shock can damage them.
