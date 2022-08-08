The MegaCD core is a MiSTer project original core developed by [srg320 (Sergey Dvodnenko)](https://www.patreon.com/srg320/){target=_blank} which aims to simulate the Sega CD / Mega CD add-on for the Sega Genesis. It uses the same [fpgagen](https://github.com/Torlus/fpgagen){target=_blank} logic and many of the improvements to it made in the MiSTer Genesis core, but adds on a significant chunk of logic that handles the powerful CD addon hardware.

## Features
* Almost all features from the [Genesis core](genesis.md)
* CUE/BIN support.
* CHD support.
* Automatic region detection.
* Multiple bios capability.
* Pier Solar support.
* [MSU-MD](https://github.com/krikzz/msu-md){target=_blank} support.

## Sega CD Mode 1 Audio - MSU-MD and Pier Solar Support

In order to use MSU-MD or to play the Sega CD version of Pier Solar on the MiSTer core the following conditions need to be met:

* The MegaDrive/Genesis cartridge ROM and the CUE/BIN (or CHD) of the whole game must be placed in the same folder.
* The MegaDrive/Genesis cartridge ROM must be renamed to `cart.rom` in order to load it into SDRAM when the CUE/CHD is loaded.
* In the case of MSU-MD, the ROM must be patched with the correct MSU-MD patch in order for it to tell the core what tracks to play and when.

If you meet all of these conditions and the game still doesn't work, then there are a few likely explanations:

1. Your ROM patch is actually an MD+ patch. MD+ is not supported at this time as a format.
2. Your ROM is not patched at all.
3. You didn't rename the cartridge's ROM to cart.rom.
4. Your cue file is incorrect.

If a set you have downloaded of MSU-MD ROMs doesn't work, then troubleshoot by applying the patch yourself to a fresh ROM to see if that works instead.
