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

## DualShock Support

More specifically, the DualShock controller mode is a catch-all solution. Ideally, it will identify what the game requires and it ought to put itself into the correct mode (either Digital or Analog) for compatibility with that game. Some games, when they are on the wrong mode, will not register inputs from your controller. If this happens, switch manually to a different mode (Digital or Analog) and see if the problem goes away.

Additionally, just like the original DualShock controller, there is a way to change between digital and analog modes on the controller at the press of a button (or multiple buttons depending on the controller you have). If you have a DualShock 4 or DualSense (5) controller, then you can just press in the touchpad in the center once. That will switch between Analog and Digital modes each time. If you do not have a controller with a PS4/PS5 touchpad on it to click, then you can use either L3+R3+Up/Down or L1+L2+R1+R2+Up/Down to changes modes, depending on the "DS mode" setting you have in the OSD.

## Fixed blanks

Due to the original playstation having a wide variety of resolution options available to software developers, and due to the fact that some of these software developers made the screen shake in their games by moving the image outside of the bounds of the screen, a solution was necessary to resolve sync loss and get appropriate scaling and stability through resolution changes. Fixed Horizontal blanks (Hblanks) and fixed Vertical blanks (vblanks) were added as options to stabilize the video output to make it more pleasant. If you experience problems with sync or the resolution changes don't look right to you, give these options a try and see if that remedies the problem.

The Vertical crop option which is made available when Fixed VBlank is turned on is similar to the 5x scaling in other cores, but due to the nature of many PSX games using either 224p or 216p, then there have been two options made available for your convenience. Try and mess around with these settings and see what looks the best to you!

## Using cheats on the MiSTer PSX core

Cheats on the PSX are a little bit different than other MiSTer cores' cheats implementation in how they are detected. With other cores, the cheat file has a CRC32 hash in the filename, and this is checked against the crc32 hash of the ROM that is loaded. This is not the case with PSX (or other CD-based cores with Cheats support either). Because CD images are so large, doing a crc32 check on them would take too long, so the internal Game ID is scanned for instead and the cheats file with the same internal Game ID is loaded. So Final Fantasy VII Disc 1 gets loaded, MiSTer detects that it is Game ID SCUS-94163, and MiSTer loads the cheats file named `SCUS-94163.zip` from `./cheats/PSX/`. Note that when the Data Cache enhancement is enabled in the OSD, cheats are disabled and will not function. This is by design.

