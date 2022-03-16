Here are some Frequently Asked Questions that you may have. If there is anything missing here, feel free to contribute by editing the page on github using the Edit pen icon in the top right.

## When will MiSTer support cartridges?
MiSTer will never use physical cartridges. 

The project aims to replace the need for having original hardware for the same experience. It is also physically impractical/impossible given the number of GPIO pins available from the FPGA. 

## Does MiSTer have lag?
It depends on your setup, but it ranges from imperceptibly low to around one frame of lag.  

Zero latency is possible with certain equipment and tweaks. [See here](../advanced/lag.md) for a more detailed explanation.

## I've seen in the news, "Update Framework".  What does that mean?
The 'framework' is all the common elements between cores that handle things like IO, video scaling, etc.

## Can I use original console controllers?
Yes, there are many USB adapters for original console controllers. They can also be connected directly via the IO board as detailed below.

## What about light guns?
Light guns such as the NES Zapper are too timing sensitive to work over USB, but will work fine on supported cores via the IO board as detailed below. 

## Any USB controller recommendations?
Almost any controller that uses USB will work with MiSTer. You can also use a Bluetooth or 2.4ghz USB adapter for wireless. Good controllers that many users seem to like and have low input latency are:

* [Sony DualSense (PS5 Controller)](https://www.playstation.com/en-us/accessories/dualsense-wireless-controller/){target=_blank} - Very low lag, fast pairing, touchpad, and extra button (mute) if paired with a bluetooth 5.0 adapter (TP-Link UB-500, Edimax BT-8500, or Asus USB-BT500 adapters are recommended and known to work).
* [8BitDo M30 Bluetooth](https://www.8bitdo.com/m30/){target=_blank} and [8BitDoM30 2.4G](https://www.8bitdo.com/m30-2-4g-for-genesis-mini-mega-drive-mini/){target=_blank} - Note these kinds of controllers do not have as many buttons as the Playstation style controllers and you may be limited if you use them.
* [8bitDo SN30 Pro 2](https://www.8bitdo.com/pro2/){target=_blank} - Versatile connectivity and confortable design that is similar to the Playstation DualShock form factor with an SNES aesthetic and button layout.
* [8bitDo Arcade Stick](https://www.8bitdo.com/arcade-stick/){target=_blank} - Wired and wireless low lag functionality with low variable lag, customizable buttons and joystick is supported.
* [iBuffalo SNES Controller](https://www.amazon.com/Buffalo-iBuffalo-Classic-USB-Gamepad/dp/B002B9XB0E/){target=_blank} - A little overpriced now, but it is a very low lag controller.

And many many more. Check [MiSTerAddons' input latency tests](https://rpubs.com/misteraddons/inputlatency){target=_blank} to help you decide. Also to ensure you get the fastest response make sure to check the [USB overclock instructions](../advanced/lag.md) section out.

There are also some excellent usb controller adapters which enable you to use original console controllers:

* [Timville Triple Controller Daemonbite](https://www.tindie.com/products/timville/triple-controller-classic-gaming-usb-adapter/){target=_blank} - A spinoff of MickGuyver's Daemonbite adapters that has support for NES, Genesis, and SNES original hardware. You can also make it yourself using instructions found [here](https://github.com/timville85/TripleController){target=_blank}. There is an option to purchase a 3d printed housing that you can also print yourself using the 3d files from [here](https://www.thingiverse.com/thing:5011783){target=_blank}.
* [MickGuyver's Daemonbite adapters](https://www.daemonbite.com/shop/){target=_blank} - Very low latency adapters, often low supply and sold out however. Can build them yourself using instructions found [here](https://github.com/MickGyver/DaemonBite-Arcade-Encoder){target=_blank} and [here](https://github.com/MickGyver/DaemonBite-Arcade-Encoder){target=_blank}.
* [2600-daptor D9](http://www.2600-daptor.com/){target=_blank} - Lowest latency "controller" in the [MiSTerAddons input latency tests](https://rpubs.com/misteraddons/inputlatency){target=_blank}.

## Can I increase the polling rate of my USB controller to improve input latency?
Yes, you can. [See here](../advanced/lag.md).

## Do I need the official USB Hub Add-On Board?
No, but you will probably want some sort of inexpensive OTG hub at least (or a regular hub with an adapter). Use a powered hub if you have many devices.

## Do I need to have a USB keyboard with me to use MiSTer?
Yes, it's a good idea to always have a USB keyboard available. Cheap wireless keyboards exist that you can use to reduce clutter.

## How do I add a second controller to MiSTer?
First setup the controller in the main menu after plugging it in with no core loaded. Then you can define it in the various cores' OSD menus.

## Does MiSTer need an IO board?
No. The IO board is optional, but offers features that could be important for some users (3.5mm and optical audio, CRT output, tape audio input, etc).

## What are the methods for connecting controllers to the serial port of the IO add-on board?
SNAC (Serial Native Accessory Converter) is used for direct wiring. Supporting cores (SNES, Genesis, NES, and TG16) allow you to directly connect original controllers. See [this page](https://github.com/blue212/SNAC){target=_blank} for details on SNAC.

## Do I need an IO board to get analog video output to my CRT?
No. You can use an HDMI to VGA adapter to do it instead. See [Direct Video](../advanced/directvideo.md).

## Is MiSTer hard to set up? Is it really only for technical people who like to tinker?
No and no, but those who enjoy tinkering can get a lot extra out of their MiSTer if they wish. The minimum setup only requires attaching a memory board to a DE-10 Nano and making an SD card. See [the Setup Guide](../setup/requirements.md) for more information.

## Which cores require SDRAM?
You can find the updated list at the [Console Cores](../cores/console.md) and [Computer Cores](../cores/computer.md) sections. Many Arcade cores use SDRAM as well.

## Why does the NES core require an SDRAM add-on board when the Genesis core does not?
The Genesis has graphics RAM and stores data that is copied from the cartridge ROM. The NES does not do this, and typically accesses the ROM directly for the data which requires much tighter timings. Using the SDRAM board on the NES core allows meeting these timing requirements.

## Does my MiSTer need cooling?
Yes, you will want at least a heatsink (passive cooling). 22mm x 22mm is the ideal size. Active cooling (a fan) helps but is not strictly required. Some faster cores like ao486 may generate a lot of heat.

## What power supply is compatible with MiSTer?
The DE10-Nano board needs a 5V power supply with at least 2A. The connector is a coaxial "barrel" plug of 5.5 mm outer diameter and 2.1 mm inner diameter, center positive. If you are using a USB Hub addon board and have a lot of power hungry peripherals attached to it (wifi, bluetooth, multiple controllers), it might be a good idea to upgrade to a similar 5v power supply, but with more amps (4A-5A).

## My MiSTer needs a case. What should I do?
There are two routes you can take; either make it yourself or purchase a case from an online vendor. For DiY, you can find the necessary 3D print files online (e.g. [thingiverse](https://www.thingiverse.com/search?q=mister+fpga){target=_blank}).

## What kind of screws do I use with the DE-10 Nano's 14mm long brass standoffs?
M3 screws, 8mm is a good length.

## How do I set up MiSTer for 1080p, shimmer free gameplay?
Run the updater script and use one of the video presets + filters that come with it in the Video Processing menu on the secondary OSD. See [Video Configuration](video.md) for more specific information.

## How do I get the scanlines filters on my MiSTer to look good?
You will need to set the device to integer scaling for best results. Either set vscale_mode=1 in mister.ini or use the vscale integer settings within the core itself (as well as 5x) if they are supported. Not all cores support the OSD options to do integer scaling.

"Integer scaling" is when your source resolution (240p) is divided into your target resolution (1080p) using only whole numbers (e.g. 1, 2, 3, 4...). This means if you use integer scaling with the MiSTer set to a 1080p resolution in the MiSTer.ini, and the core you are using natively outputs 240p, then the image will be scaled 4x which 4 times 240 equals 960. This leaves a black border for the remaining 80 pixels distributed across the top and bottom the screen.

You can play with other settings if you want the scaler to fill the screen, but scanlines won't be "perfect" unless the source resolution (e.g. 240p) divides evenly into the target resolution (e.g. 1200p at 5x scaling).

## I have a 4k or other higher than 1080p display, does MiSTer support that resolution?  I'd like to enjoy better video scaling.
MiSTer can't quite reach 4k. Edit mister.ini on your SD card to change resolutions, e.g. video_mode=12 for 1440p or video_mode=13 for 1536p (hardware maximum). Compatibility with these higher resolutions may depend upon your display and signal chain.

## How does the accuracy level of various MiSTer cores compare to other FPGA options?
Most MiSTer cores are just as, if not more accurate, as any of the other major FPGA offerings available today. Most people would not able to tell the difference between these cores and the original hardware.

## Will any MiSTer core ever get save states?
The Gameboy, GBA, Lynx, and NES core supports save states.

Cores need to be written from scratch to support them (as was done with the GBA and Lynx cores) or they need to be reworked to support pause before save states can be added (as was done with the Gameboy and NES cores). At this time there are no specific plans to apply this to other cores, but it may happen one day.

## Why doesn’t this core from another repo work? Why is MiSTer so hard to use?
MiSTer repositories are self contained and the official updater script only fetches cores from the active official MiSTer repositories. Cores from other repos are not fully integrated so your results may vary. Some developers have their own discord servers or forums and you can seek support there.

## When is an N64 core coming?
Probably never. There isn’t really sufficient bandwidth.

## When is PlayStation core coming?
Probably next year. Serious progress has been made by a few developers but there’s no official ETA.

##  Other cores work but I get a black screen for this one. What do I do?
Try setting vsync to 0 as your display may not support all refresh rates. (Note that this was the default setting.)

## My CD games don’t work! Help!
Unzip them. Do not zip CD games. Also put them in iso/wav/bin/img + cue format.

## What version of the CD card bios do I need for TG16 CD?
Use Japanese version 3.0. You will commonly find it with filename: `Super CD-ROM System (Japan) (v3.0).pce`

## How do I make MisTer boot into the NES core and a specific game?
You need to use two different options: autobooting a core, and starting the core on a given ROM. Here is how:
In the .INI file, set `bootcore=NES_20201102.rbf` (or the specific core version you have), and comment out `;bootcore_timeout`.
Then on your NES games folder (e.g. `/media/fat/games/NES/`, copy the FDS bios as `boot0.rom`, and your .NES rom to boot as `boot1.rom`.
For more options, please refer to the [NES core documentation](https://github.com/MiSTer-devel/NES_MiSTer#installation){target=_blank} 

## I heard the DE10-Nano board uses subsidized components. Is MiSTer doomed if that stops?
De10-Nano is manufactured in very large scale for use by students and is widely available. When it reaches end of life, the open source cores and infrastructure will be ported to another widely available board.

## I see a defect that some other people aren’t seeing. Should I get a different DE-10 Nano?
No, you should report the defect and wait for a fix. There is no magical best DE-10 Nano.

##  I found some other Cyclone based dev board on sale and it has built in WiFi. Can I use it for MiSTer?
Generally, no. While it’s always possible that someone will take time to port things to other boards, the different pins and memory will mean it won’t be a straight use and unless it’s a significant upgrade, it would never gain official support.

## The DE-10 is rated for up to 100°C operation and it doesn’t get nearly that hot.  Do I really need a fan or heatsink? 
A number of complex cores (like ao486) benefit from having the chip at cooler temperatures, since heat can affect the tight timings they require. A fan is recommended to avoid any possible glitches, but you won't damage your DE10-Nano if you choose not to use one.

## Can you take screenshots on the MiSTer?
You can take screenshots on the MiSTer very easily. All you have to do is press `Win + PrtScr` on your keyboard and you will get an upscaled screenshot. For raw output from the core (which may be distorted or in a weird aspect ratio) prese `Shift + Win + PrtScr`. The screenshots are stored in `./screenshots` in a folder named after the core you took the screenshot in.

These screenshots do include the effects of any video processing options, they are very simple. To take screenshots of the full video processing (i.e. the image you see on your modern screen when using the MiSTer) you will need to use some kind of capture card that supports the desired resolution.

[Here is an example of a raw screenshot from the NES core](img/raw_screenshot.png){target=_blank}

[Here is an example of an upscaled screenshot from the Neo Geo core](img/upscaled_screenshot.png){target=_blank}
