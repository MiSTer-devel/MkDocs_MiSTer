The Sony Playstation (PSX) MiSTer core is the most feature-filled and heavily developed core thus far. Multiple controller options, automatic bios region swapping, both memory card slots with manual memory card file loading, modes to increase the speed, and even modes to modify the textures in-game. This core by Robert Peip ([FPGAzumSpass](https://www.patreon.com/FPGAzumSpass/){target=_blank}) took a huge amount of work and is still being worked on actively due to the large task that is writing a PSX emulator in general. Here we will highlight some of the features of the PSX core.

## Controller Support

The MiSTer PSX core supports a very large list of control options that original hardware had available to it.

* [DualShock](https://en.wikipedia.org/wiki/DualShock#DualShock){target=_blank} (Later controller with analog sticks and rumble/vibration capability)
* [Digital Pad](https://upload.wikimedia.org/wikipedia/commons/f/f9/PSX-Original-Controller.jpg){target=_blank} (original PSX controller without analog sticks)
* Analog Pad mode (dual analog sticks mode enabled)
* [GunCon](https://en.wikipedia.org/wiki/GunCon#GunCon){target=_blank}
* [NeGcon](https://en.wikipedia.org/wiki/NeGcon){target=_blank} (Can also be used as a Steering Wheel using the "Wheel-NegCon) option in the OSD.)
* Racing Wheels (some analog racing wheels can be used if you switch to "Wheel-Analog" in the OSD.)
* [Mouse](https://en.wikipedia.org/wiki/PlayStation_Mouse){target=_blank}
* [Justifier](https://en.wikipedia.org/wiki/Konami_Justifier){target=_blank}
* SNAC (there is a special adapter required to use real PSX controller accessories. Memory cards and even the pocketstation can be used in this mode technically)
* [Analog Joystick](https://en.wikipedia.org/wiki/PlayStation_Analog_Joystick){target=_blank}
* [Pop'n Music Controller](https://www.resetera.com/threads/popn-music-ot-button-slapping-intensifies.3419/){target=_blank}

### DualShock Support

More specifically, the DualShock controller mode is a catch-all solution. Ideally, it will identify what the game requires and it ought to put itself into the correct mode (either Digital or Analog) for compatibility with that game. Some games, when they are on the wrong mode, will not register inputs from your controller. If this happens, switch manually to a different mode (Digital or Analog) and see if the problem goes away.

Additionally, just like the original DualShock controller, there is a way to change between digital and analog modes on the controller at the press of a button (or multiple buttons depending on the controller you have). If you have a DualShock 4 or DualSense (5) controller, then you can just press in the touchpad in the center once. That will switch between Analog and Digital modes each time. If you do not have a controller with a PS4/PS5 touchpad on it to click, then you can use either L3+R3+Up/Down or L1+L2+R1+R2+Up/Down to changes modes, depending on the "DS mode" setting you have in the OSD.

## Manual Memory Card Loading

You can load Playstation memory card files (.mcd or .sav) manually in the OSD in this core. It is probably best to use the 2nd slot because the default behavior is to occupy the first slot automatically with a blank memory card file. You can also opt out of auto-mounting a blank memory card file to slot 1 by turning off the Automount Memory Card 1 option in the OSD. Finally, if you have a SNAC adapter with a memory card slot connected to it somehow, the core does support real Playstation 1 memory card loading over SNAC.

## Libcrypt Support

Some games used a kind of copy protection with what was called "Libcrypt" and they will not work if it's not circumvented.

You can provide an .sbi file to do that. If there is an .sbi file [(the whole collection can be downloaded from redump.org)](http://redump.org/sbi/psx/){target=_blank} next to a .cue with the same name, it will then be loaded automatically when mounting the CD image. The MiSTer updater automatically downloads these .sbi files so it should not be necessary to download and place them manually.

## Audio and Video Options

### Fixed blanks

Due to the original playstation having a wide variety of resolution options available to software developers, and due to the fact that some of these software developers made the screen shake in their games by moving the image outside of the bounds of the screen, a solution was necessary to resolve sync loss and get appropriate scaling and stability through resolution changes. Fixed Horizontal blanks (Hblanks) and fixed Vertical blanks (vblanks) were added as options to stabilize the video output to make it more pleasant. If you experience problems with sync or the resolution changes don't look right to you, give these options a try and see if that remedies the problem.

It should also be noted that Fixed Horizontal blanks makes everything fit within the original 4:3 aspect ratio of the PSX video output, so it should be turned on in pretty much all situations if you want the original resolution.

The Vertical crop options, which are made available when Fixed VBlank is turned on, is similar to the 5x scaling in other cores, but due to the nature of many PSX games using either 224p or 216p, then there have been two options made available for your convenience.

The Horizontal Crop option is made for some PAL games, see what works best for you.

A good example of a game that benefits from the Fixed Horizontal Blanks option is Metal Gear Solid. The shaking of the screen in some scenes would cause your modern display to lose sync without the Fixed VBlank option turned on.

A good example of a game that benefits from the Fixed Vertical Blanks option is Final Fantasy VII. Horizontal blanks gives you the proper 4:3 aspect ratio first of all, but then will give you a "jump" in the resolution when it changes from world map to the battle screen. However, when used in conjunction with Vertical Crop -> On(224/270), you will notice that the transition from the world map to a battle will no longer make a jarring resolution change where the screen position seems to change. Here's an example video that shows the benefits:

![type:video](videos/psx-blanks-ff7.mp4)

There are more examples like this out there, you will have to test for yourself to see what works best.

### Black Transitions

Some resolution and screen transitions are so quick that the framebuffer on the MiSTer is not cleared out completely in DDR3, so this is a workaround to not show ghost images from previous frames over scaled video (hdmi or vga_scaler).

### Deinterlacing Methods

The MiSTer PSX core supports two methods of deinterlacing the occasional interlaced video on the Playstation. Weave is the default and is often preferred, this gives you the most stable image. Bob is very jittery, but may look better on real CRT's in some situations.

### Sync 480i for HDMI

This option syncs the 480i output for when you are playing on an HDMI display. It will improve the speed at which the resolution changes from 480i to 240p for many displays.

### Rotate

If for whatever reason you need to rotate your screen 180° you can just go to the Audio and Video options in the OSD and toggle "Rotate" to On or Off.

### Dithering On/Off Toggle

You can optionally toggle Dithering On and Off. In some games this can cause color banding which can look undesirable, in others it can clean up the checkerboard look without much loss. You will have to find out what is most appropriate.

### Render 24 bit

Enables 24 bit rendering, which may make same games appear much smoother in the graphics and not require dithering to avoid color banding issues. Try it out.

### Dither 24 bit for VGA

MiSTer's analog IO board was not originally designed for 24-bit RGB color representation in mind. As a result only 18-bit video comes out over the analog IO board. This option will dither 24-bit video sources from the PSX (most situations are not 24-bit, usually just FMV sequences from some games) so the lack of those 6 bits is not apparent over analog video. This has no effect on HDMI video and shouldn't be used if you are using a direct video adapter, which has full 24-bit RGB support.

### 480i to 480p Hack

This option does a hack to convert 480i to 480p. It may look buggy in some games, but the point is for some 480i 3d games to not look so jittery and to not have horizontal lines interrupting the image.

### Widescreen Hack

The MiSTer PSX core has a Widescreen hack mode. There are many games which are 3d only with very little 2d, so you could potentially stretch the visible landscape and not stretch the 3d models. Some games work well with this, while others do not. Your results may vary. There are multiple Aspect Ratios for this hack to leave some options open for various displays and games, 3:2, 5:3, and 16:9 (what most modern displays are). Here's an example using R4 - Ridge Racer Type 4:

![type:video](videos/psx-widescreen.mp4)

### Texture Filter

The Playstation didn't have any built-in texture filtering like some other consoles did (Nintendo 64 is a popular example). This means many of the textures had rough edges. In some cases this is fine, but in some games it can be very displeasing. This little trick in the MiSTer PSX core allows you to smooth out the textures on 3d objects if you wish. A good example where this could be used is in Tony Hawk's Pro Skater 2, like in the video below:

![type:video](videos/psx-texturefilter.mp4)

### SPU RAM select

The MiSTer PSX core is the first released core which supports the optional Dual SDRAM modules. This was necessary early in it's development as there wasn't enough bandwidth on one SDRAM module to contain both the test roms and small games and to store other components that were needed to be placed in SDRAM at the same time. You are not required to have Dual SDRAM on the PSX core for quite some time now, and the official release is a Single SDRAM build that is compatible with the Analog IO board.

Toggling this option while a game is running will most likely crash the game. If you have a Dual SDRAM build of the core and you enable this option, you will likely have to reset the game to get it to work.

There is only one humanly imperceptible difference in using the Dual SDRAM build of the MiSTer PSX core known. The audio samples are measurably more accurate to a tiny fraction of a millisecond. The human ear can't tell that 1 or 2 out of 44,100 samples per second were dropped.

This option to use Dual SDRAM for the SPU is disabled by default in the regular releases of the core. To get a special release with Dual SDRAM support currently you can either open the Quartus Project File (.qpf) with the name "PSX_DualSDRAM.qpf" using Quartus 17.0.2 and compile the core, or you can get the latest Test Build from the [MiSTer FPGA Discord](https://discord.com/misterfpga){target=_blank} in the #test-builds channel.

## Miscellaneous Options

These are the speedhacks in the MiSTer PSX core which will allow you to improve the performance of Playstation games, while potentially sacrificing some compatibility.

### Fastboot

Fast boot bypasses the BIOS boot logo and screen when starting a game. This can make it a lot quicker to get into the game, however there are a small number of games where it may lead to bugs and other compatibility issues. If you notice bugs in a game, try to turn off fastboot before submitting a bug report about the core first.

### Unsafe Options

The core offers various options to improve gameplay for some games, but those options cannot be considered stable through all games. If you use one or more of these options, the core will warn you every time you start a game.

* **480i to 480p hack:** Allows to render some games with full 480p resolution, removing interlacing artifacts. Only works for some full 3D 480i titles.
* **Turbo:** Increases CPU, DMA, Memory and GTE performance by ~10%(Low), ~20%(Medium) or 50%(High). Cheats cannot be used while Turbo is on and are disabled automatically.
* **Pause when CD slow:** CD data must be returned in a fixed time frame, otherwise the core will pause until the data has arrived. Disabling this will remove these pauses, but also risk that the game hangs up due to CD data being late.
* **PAL 60Hz Hack:** Runs PAL games with 60Hz. PAL Games will often run faster with this hack on. Screen height is limited to 256 lines in this mode, so some games might be cropped.
* **CD Fast Seek:** CD will seek the next sector in the minimal possible time. Decreases loading time of games, but some games depend on the long loading times and will crash.
* **CD Speed:** Allows to run the CD drive with fixed higher speed to decrease loading times, but some games depend on the long loading times and will crash. CD will automatically speed down to original speed for FMVs or CD audio playback and back to increased speed in loading areas. The higher speed rates are more unstable and require proper storage to be usable with bin/cue files reaching higher performance than chd.
* **Limit Max CD Speed:** Will hold back any new CD data until the game has processed the last data. Mostly useful to prevent CD data overrun when using higher speed modes, leading to overall faster loading times due to less read retries.
* **RAM:** 8 Mbyte option from development consoles. Only use for homebrew that requires it, otherwise there is a high chance of crashing games.
* **GPU Slowdown:** Slows down GPU Fillrate.

### Overlays

By default there are 3 information overlays that are disabled, you can enable them if you want to:

* FPS Overlay - Frames per second.
* Error Overlay - Error messages mentioned above.
* CD Slow Overlay - Displays an indicator that the cd access time is slower than expected. If you are using a spinning hard disk or are using a NAS for your ROM storage the core will pause and wait for data if there is an unexpected delay. This indicator shows when this occurs.

## Using cheats on the MiSTer PSX core

Cheats on the PSX are a little bit different than other MiSTer cores' cheats implementation in how they are detected. With other cores, the cheat file has a CRC32 hash in the filename, and this is checked against the crc32 hash of the ROM that is loaded. This is not the case with PSX (or other CD-based cores with Cheats support either). Because CD images are so large, doing a crc32 check on them would take too long, so the internal Game ID is scanned for instead and the cheats file with the same internal Game ID is loaded. So Final Fantasy VII Disc 1 gets loaded, MiSTer detects that it is Game ID SCUS-94163, and MiSTer loads the cheats file named `SCUS-94163.zip` from `./cheats/PSX/`. Note that when the Data Cache enhancement is enabled in the OSD, cheats are disabled and will not function. This is by design.

## Error Messages

If there is a problem recognized by the MiSTer PSX core, an error overlay is displayed, showing which error has occured. You can hide these messages with the "Error Overlay" OSD option, by default they are on.

List of error codes:

* `E2` - CPU exception(only relevant if game shows issues)
* `E3` thru `E6` - GPU hangs (e.g. corrupt display list)
* `E7` - CPU2VRAM with mask-AND enabled
* `E8` - DMA chopping enabled
* `E9` - GPU FIFO overflow
* `EA` - SPU timeout
* `EB` - DMA and CPU interlock error
* `EC` - DMA FIFO overflow
* `ED` - CPU Data/Bus request timeout -> will also appear if the BIOS is not found or corrupt or no SDRAM module is installed
* `EE` - Dotclock used as timer report(only relevant if game shows issues)
* `EF` - BusWidth for SPU was set to 8 Bit (but should be 16 bit)
