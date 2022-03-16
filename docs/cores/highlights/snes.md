The Super Nintendo Entertainment System (or SNES) MiSTer core has multiple features like CPU and Super FX chip turbo mode, lightgun support, mouse support, and even changing the WRAM initialization value. In addition to this, it also has support for nearly every single enhancement chip released. It is a very powerful core that was primarily developed by [srg320](https://www.patreon.com/srg320){target=_blank} when he didn't even have original hardware.

## Enhancement Chip Support
Here are the SNES enhancement chips currently supported with some example games they were used in:

* Super FX AKA GSU-1 (Star Fox, Star Fox 2, Stunt Race FX)
* Super FX 2 AKA GSU-2 (Super Mario World 2: Yoshi's Island, Doom)
* CX4 (Only in Mega Man X 2 and Mega Man X 3)
* DSP-1 (Super Mario Kart and Pilotwings)
* DSP-2 (Only in Dungeon Master)
* DSP-3 (Only in SD Gundam GX)
* DSP-4 (Only in Top Gear 3000)
* OBC-1 (Only used in Metal Combat: Falcon's Revenge)
* S-DD1 (Only used in Star Ocean and Street Fighter Alpha 2)
* SA-1 (Kirby Series, Super Mario RPG)
* SPC7110 (Far East of Eden Zero, Large Shell beast Story 2)
* ST1010 (F1 Roc 2 - Race of Champions)
* S-RTC (Daikaiju Monogatari II)

Currently the only enhancement chips not supported are GB-Z80 (Super Game Boy), MX15001TFC (Nintendo Power Flash Cartridges), ST011 (Hayazashi Nidan Morita Shougi), and ST018 (Hayazashi Nidan Morita Shougi 2). This is mostly because the core is already near the limit of what the DE10-Nano's Cyclone V is capable of fitting into it's design.

### SNES Enancement Chip Example Video
![type:video](videos/snes-chips.mp4)

## Satellaview Support
This core also supports Satellaview. You just need the BSX/BS-X rom placed into the `./games/SNES/` folder and renamed to `bsx_bios.rom`. The core used to require patched versions of the rom to run, but every original Satellaview ROM that didn't require an internet connection, extra peripherals, or something like that will run now without patches.

### BS-X Satellaview Example Video
![type:video](videos/snes-bs-x.mp4)

## Super FX Turbo
The MiSTer SNES core has a Super FX Turbo option which overclocks the Super FX chip so games run a little faster. Combined with the Turbo CPU option games like Star Fox will have a higher framerate. However, the game will run faster than intended so your results may vary. It is also important to note that the use of such hacks may increase the likelihood of bugs occurring, so please do not report bugs when using Turbo options.
### Super FX Turbo Example Video
![type:video](videos/snes-fx-turbo.mp4)
