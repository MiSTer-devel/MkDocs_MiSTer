The Nintendo Entertainment System (NES) MiSTer core is packed full of many features to be explored. There are options like automatic Famicom Disk System (FDS) disk swapping, custom palette loading, overscan and screen edge masking, extra sprites hack, and SNAC (so you could use an original Zapper lightgun on a CRT with analog video output).

## Extra Sprites mode
Some NES games would allow more sprites on the screen than the system was typically designed to allow at one time and the sprites would flicker to keep them on the screen. There was a limit to how many sprites could be on the screen at one time. The NES MiSTer core lets you somewhat remove this limit, reducing the amount of flicker that occurs when many sprites are on the screen in games like Rygar. This does not work with all games that have flicker, some flicker was added intentionally by the original developers for other reasons.

### Extra Sprites (deflicker) Example Video
![type:video](videos/nes-flicker.mp4)

## Palettes
The NES core has both built-in palettes and the ability to load custom palettes. You may be wondering why the NES core needs palettes. It's just colors, right? Without going into it here, if you want to learn about NES Palettes, watch [this YouTube video by NesHacker](https://www.youtube.com/watch?v=7Co_8dC2zb8), and read the pinned comment there as a couple details were technically inaccurate. Basically, the NES does not have a native palette of colors to work with as the colors were not output in the typical red, green, and blue values like other game consoles. So emulators need to come up with palettes that most closely approximate the original viewing experience. This viewing experience would sometimes vary depending on the tv you were watching on, so multiple palette options are made available. This also makes it possible to do fun and ridiculous palettes just for the sake of it, like the virtual boy palette made by RetroSho.

### Palettes Example Video
![type:video](videos/palettes.mp4)

## Famicom Disk System BIOS boot.
[Download Blank FDS boot2.rom](files/boot2.rom){target=_blank} and then place this in `./games/NES/`. Then when you start the core (assuming you already have the FDS bios placed there and renamed to `boot0.rom`) it will boot to the FDS BIOS as if you had a blank disk inserted.

### Famicom Disk System Blank Disk Boot Example Video
![type:video](videos/fdsbios.mp4)