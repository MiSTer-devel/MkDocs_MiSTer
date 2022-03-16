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
