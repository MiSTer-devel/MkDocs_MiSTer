The Genesis core is a port of the [fpgagen](https://github.com/Torlus/fpgagen){target=_blank} core to MiSTer, with significant enhancements and additions.

## Features
* Composite Blending effect (e.g. Sonic Waterfall transparency)
* CPU Turbo option (e.g. Road Rash gameplay speed)
* Increase sprite limit.
* Audio Filtering options for Model 1, Model 2, Minimal, and No Filter
* Switch between YM2612 (Model 1) or YM3438 (Model 2/3) FM Synth
* Multitap: 4-way, Team Player, J-Cart
* SVP Chip (Virtua Racing for Genesis supported)
* Auto-Region header detection using the [new style and the old style combined](https://plutiedev.com/rom-header#region){target=_blank}.
* Corrected Aspect Ratio option for 320x224 game resolutions (e.g. Castlevania Moon).

## Region detection
There are two methods of region detection.

1. Header: This method detects a character in the header to determine if the game was intended to be played on a Japanese, European, or American version of the console. This method is default and preferred as it is compatible with the entire commercial lineup. This option uses a region priority setting for multi-region games which had "JUE" in the header. Whatever the first region is, will be the region set on load of a multi-region game.

2. File Ext: This method changes the region according to the filename extension of the rom. 
    * BIN = Japanese
    * GEN = America
    * MD = Europe

There is also a region priority list for multi-region games that had multiple region codes in the header. This is useful if you want to specify a certain region to default to in order of first priority to last (e.g. US>JP>EU will try to load multi-region games in US first, then it will load as JP if no US region code is present, then EU if neither is present).

## Corrected Aspect Ratio Example Video
![type:video](videos/genesis-car.mp4)

## Composite Effect Example Video
![type:video](videos/genesis-comp.mp4)

## Turbo CPU Example Video
![type:video](videos/genesis-turbo.mp4)
