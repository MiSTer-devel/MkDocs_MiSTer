---
hide:
  - toc
---

In MiSTer terminology, a "core" is the current system that the FPGA is configured to simulate. It is configured as the "Menu" core when you power on the MiSTer for the first time. Then, if you use the OSD and go to `_Console` and then select `NES`, it will configure the FPGA to be the "NES" core.

The term "core" has been used by Hardware Description Language (HDL) developers in a way which refers to the things that are programmed onto the FPGA. So for instance, the MiSTer FPGA framework uses Intel's "Altera PLL Core". This is a chunk of logic that is portable which allows developers to hook up to the clock on the chip. There are HDMI cores, ethernet cores, serial data cores, and so on...

However, for MiSTer, a core refers to the system being emulated. So you have the [PSX (Playstation) core](https://github.com/MiSTer-devel/PSX_MiSTer){target=_blank}, the [Minimig (Amiga) core](https://github.com/MiSTer-devel/Minimig-AGA_MiSTer){target=_blank}, the [SNES core](https://github.com/MiSTer-devel/SNES_MiSTer){target=_blank}, and so many more to explore.

## What happens when I load a core?

Imagine every time you load a core you are connecting a different console, computer, or arcade system to your television. You select the Genesis core in the menu and load it, you have now essentially plugged a Genesis into your television without all the hassle of wrestling with cables. That's the concept. What actually is happening is that `.rbf` file is reprogramming the FPGA chip to take on a different form. It used to contain the digital logic required to be an NES combined with the MiSTer FPGA core components, and it turned into a chip with the digital logic for the Genesis combined with the the MiSTer FPGA core components.

Now, you may be worried that all of this rewriting of the FPGA could reduce it's lifespan. This isn't something to worry about, these kinds of FPGA's (SRAM-based) are considered to have an indefinite number of writes. Many millions of rewrites to the same sector are normal and nothing to worry about.

## Core updates and issues

Cores on MiSTer are the result of the collaboration between many people and extensive testing, sometimes over many years and prior open-source projects. Most console and computer cores have now been compared to original hardware to a high level of precision (e.g. audio capture comparison), with the few issues remaining documented on their respective github repository pages. Please refer to these pages, per core, before submitting any issues.

For a list of core repositories, head on over to the [MiSTer FPGA GitHub Organization Repositories list](https://github.com/MiSTer-devel){target=_blank} for more information. The core links there will bring you to the release folder on github, which will also allow you to find the Issues page and the readme files, ideally listing all available features and limitations in detail per core.

There are other unofficial MiSTer FPGA cores out there, but these are not listed here as they may or may not work correctly and that list is always changing.
