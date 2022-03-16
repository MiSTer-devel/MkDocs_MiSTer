MiSTer has various addon boards that are somewhat optional to use such as a 128MB SDRAM add-on board that allows you to use all of the cores on the system and the Analog IO board which enables you to easily connect your MiSTer to a classic CRT telivision or monitor. These boards can be purchased by various sellers online or assembled yourself by ordering the PCB from a PCB manufacturer, buying the components online, and soldering it yourself. 

Here's a rundown of what the current add-on boards are and what they do.

## [128MB SDRAM Addon Board](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/sdram_xsds_2.9.pdf){target=_blank}

![](img/sdram.png)

The 128MB SDRAM Add-on board for MiSTer is essential for multiple cores to even load games. You can alternatively go with a 32MB SDRAM board for a cheaper price, however there are some games on Neo Geo, Game Boy Advance, and a few other cores which might no be compatible if you go with the smaller sized module.

## [USB Hub Addon Board](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/USBHub_2.1.pdf){target=_blank}

![](img/usbhub.png)

The USB Hub Add-on board for MiSTer has two methods of connecting to your DE10-Nano either via internal headers with a slim external board or with a bridge to connect both MicroUSB ports together. This board provides an OTG USB Hub for the Mister which has one power-only usb port in the back and 6 USB 2.0 ports ont he other 3 sides. It requires power so you may need a power splitter to supply power to both the DE10-Nano and this USB hub. If you use a Digital IO board you will only need a DC to DC jumper cable and a single cable to the Digital IO board's barrel jack in order to power the whole stack.

## [Digital I/O Addon Board](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/iobrd_dig_1.2.pdf){target=_blank}

![](img/digitalio.png)

Get this board if you want a few more options. It is cheaper than the Analog IO board below typically, and it leaves the 2nd SDRAM slot unoccuppied for the potential future cores which may require it someday.

* 3 Buttons, Reset, On-Screen Display (OSD), and User (for various user interactions without a keyboard)
* 3 status LEDs, Power, Disk, and User
* Secondary MicroSD card slot that may be required by some older computer cores. This is not typical MicroSD storage, think of it as like a little floppy drive.
* Mini-TOSLINK optical digital audio port.
* Full size TOSLINK optical digital audio port.
* User IO Port. This is a port that **looks** like it is USB 3.0 but it **is not!** This is actually used for direct serial communication with various peripherals and adapters like [SNAC adapters](https://github.com/blue212/SNAC){target=_blank} and [MT32-Pi](https://github.com/dwhinham/mt32-pi){target=_blank}.
* Fan Power header and fan mounting holes for better cooling.
* **Doesn't** use the 2nd set of 2x20 headers on the DE10-Nano so it is compatible with Dual SDRAM configurations.

## [Analog I/O Addon Board](https://github.com/MiSTer-devel/Hardware_MiSTer/raw/master/releases/iobrd_6.1.pdf){target=_blank}

![](img/analogio.png)

Get this board instead of the Digital IO Addon board if you want to use your MiSTer for simultaneous video output to a CRT and HDMI monitor. Otherwise the cheaper Digital IO board should be sufficient.

* 3 Buttons, Reset, On-Screen Display (OSD), and User (for various user interactions without a keyboard)
* 3 status LEDs, Power, Disk, and User
* Power On/Off Switch.
* Barrel jack which can be used to power the DE10-Nano with.
* Secondary MicroSD card slot that may be required by some older computer cores. This is not typical MicroSD storage, think of it as like a little floppy drive.
* VGA port for analog video output - See [Advanced - CRT](../advanced/crt.md) for the potential connectivity options.
* Simultaneous analog video and HDMI video output is possible with this board.
* Sync-on-green override\auto switch.
* 3.5mm analog audio port that is also a Mini-TOSLINK optical digital audio port at the same time.
* 3.5mm audio-in port for ADC-in (like Tape input for some computer cores).
* User IO Port. This is a port that **looks** like it is USB 3.0 but it **is not!** This is actually used for direct serial communication with various peripherals and adapters like [SNAC adapters](https://github.com/blue212/SNAC){target=_blank} and [MT32-Pi](https://github.com/dwhinham/mt32-pi){target=_blank}.
* Fan power header and fan mounting holes for better cooling.
* Uses the 2nd set of 2x20 headers on the DE10-Nano so it is **not** compatible with Dual SDRAM configurations.

## [MT32-Pi Lite MiSTer Addon Board](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/MT32Pi_lite.pdf){target=_blank}

[MT32-Pi](https://github.com/dwhinham/mt32-pi/wiki){target=_blank} is a baremetal emulator of the Roland MT-32 synth module. This add-on board is Sorgelig's rendition of the new version that utilizes a Raspberry Pi Zero 2 W. Get this board if you want to listen to upgraded Midi sounds in certain cores and games that support it, like the ao486 core or the X68000 core. Here's a video by youtuber MiSTer Walrus FPGA [showing off how the MT32-Pi sounds](https://www.youtube.com/watch?v=q05ud_eNU8E){target=_blank}.

## [Real Time Clock](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/rtc_1.3.pdf){target=_blank}

There is a Real Time Clock add-on board if you want to add a real-time clock to your MiSTer. Some computer cores use this feature if you are interested.