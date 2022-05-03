---
hide:
  - toc
---

This is a compatibility chart that shows the default Analog video output of MiSTer's cores. This list needs to be updated, it is possible that not every single core matches this list entirely. If you have a computer CRT monitor, any 15kHz core can be scandoubled for compatibility. If you have a consumer CRT television, any 31kHz core likely has a custom video_mode (also called modeline) that could be used to trick your TV into displaying the otherwise 31kHz output with varying success.

This is list is not to be taken as a literal hard authoritative source, it is community sourced and is a living document. If your core is not compatible with your display, then try other options, don't give up just because of this list.

## Table of cores and resolutions supported over the RGB/VGA output

### Consoles

|Core|Version|Native Resolution|Frequency (Horizontal, Vertical)|Notes|
|--- |--- |--- |--- |--- |
|Atari2600|20181214|240p|15.40kHz, 59.4Hz|A startup rom must be placed in the core|
|Astrocade|20181224|240p|15.70kHz, 59.9Hz||
|Atari5200|20180819|240p|15.62kHz, 59.9hz||
|Colecovision|20181130|240p|15.49kHz, 59.7Hz||
|Gameboy|20200331|240p|15.77kHz, 59.7Hz|Enable "Stabilize video" to prevent sync issues on blank screens|
|GBA|20200409|240p|15.77kHz, 59.7Hz||
|Genesis|20200502|240p|15.72kHz, 59.9Hz||
|NeoGeo|20200325|240p|15.63kHz, 59.2Hz||
|NES|20200308|240p|15.75kHz, 60.1Hz||
|Odyssey2|20181221|240p|15.61kHz, 60.1Hz||
|SMS|20200309|240p|15.7kHz, 59.9Hz||
|SNES|20200306|240p|15.75kHz, 60.1Hz||
|TurboGrafx16 (PC Engine)|20181231|240p|15.56kHz, 59.7Hz||
|Vectrex|20180616|VGA|44.96kHz, 60.0Hz||

### Computers

|Core|Version|Native Resolution|Frequency (Horizontal, Vertical)|Notes|
|--- |--- |--- |--- |--- |
|Acorn Archimedes|20180519|240p|16.22kHz, 52.2Hz||
|Altair 8800|20181113|VGA|45.03kHz, 60.0Hz||
|Amiga|20181216|240p|15.68kHz, 50.4Hz||
|Amstrad CPC 6128|2018084|240p|15.63kHz, 50.25Hz|boot rom needed|
|486|20181215|VGA|44.95kHz, 60.0Hz||
|Apogee|20180305|240p|15.44kHz, 50.0Hz||
|Apple II+|20180308|VGA|30.62kHz, 58.5Hz||
|Apple Macintosh Plus|20180305|Mac|22.06kHz, 60.1Hz||
|Aquarius|20180429|240p|15.49kHz, 59.6Hz||
|Atari 800|20180812|240p|15.63kHz, 59.9Hz||
|Atari ST|1|VGA|31.13kHz, 49.9Hz||
|BBC Micro|20180521|?|62.5kHz, 62.5kHz||
|BK0011M|20180901|240p|15.82kHz, 48.82Hz||
|Commodore 64|20180831|240p|15.31kHz, 58.4Hz||
|Commodore 16|20180902|240p|15.50kHz, 49.8Hz||
|Commodore PET|20180305|240p|15.49kHz, 59.6Hz||
|Commodore VIC-20|20180926|240p|15.54kHz, 59.8Hz||
|PDP-1|20190101|1280x1024|63.80kHz, 59.9Hz||
|MSX|20180520|240p|15.62kHz, 59.9Hz||
|MultiComp|20180629|VGA|30.99kHz, 59.6Hz||
|Sharp MZ Series|20180927|240p|15.01kHz, 58.0Hz|no HDMI output|
|Sinclair QL|20180305|240p|15.74kHz, 60.3Hz||
|Specialist/MX|20180305|yes|15.61kHz.50.0Hz||
|Tandy CoCo3|091918a|VGA|31.28kHz, 59.9Hz||
|TI-99/4A|20180527|240p|15.38kHz, 59.88Hz|A startup rom must be placed in the core|
|TSConf|20180901|240p|15.51kHz, 50.0Hz||
|Vector 06C|20180304|240p|15.51kHz, 50.0Hz||
|X68000|20171103|NA|NA||
|ZX Spectrum|20181231|240p|15.51kHz, 48.8Hz||
|ZX81|20180903|240p|15.62kHz, 59.9Hz||

### Arcade

|Core|Version|Native Resolution|Frequency (Horizontal, Vertical)|Notes|
|--- |--- |--- |--- |--- |
|1942|20180313|VGA|37.77kHz, 60.3Hz|TATE, image squished over HDMI|
|Alibaba|20180313|240p|15.49kHz, 59.1Hz||
|Amidar|20180313|240p|15.86kHz, 60.6Hz||
|AzurianAttack|20180313|240p|15.86kHz,  60.6Hz||
|Bagman|20180313|240p|15.86kHz, 60.6Hz||
|BlackHole|20180313|240p|15.86kHz, 60.6Hz||
|BombJack|20180313|240p|15.49kHz, 59.1Hz||
|Bubbles|20181217|240p|15.49kHz, 59.1Hz||
|BurgerTime|20180313|240p|15.49kHz, 59.1Hz||
|BurningRubber|20180313|240p|15.49kHz, 59.1Hz||
|Catacomb|20180313|240p|15.49kHz, 59.1Hz||
|Colony7|20181218|240p|15.49kHz, 59.1Hz||
|ComputerSpace|20180313|240p|15.49kHz, 59.1Hz|menu not available over VGA|
|CosmicAvenger|20180313|240p|15.89kHz, 61.1Hz||
|CrazyClimber|20180607|240p|15.49kHz, 59.1Hz||
|CrazyKong|20180313|240p|15.49kHz, 59.1Hz||
|CrushRoller|20180313|240p|15.49kHz, 59.1Hz||
|Defender|20180313|240p|15.49kHz, 59.1Hz||
|DonkeyKong|20180418|240p|15.86kHz, 60.6Hz||
|Dorodon|20180313|240p|15.86kHz, 60.6Hz||
|DreamShopper|20180313|240p|15.86kHz, 60.6Hz||
|Eeekk|20180313|240p|15.86kHz, 60.6Hz||
|Eyes|20180313|240p|15.86kHz, 60.6Hz||
|Frogger|20180313|240p|15.86kHz, 60.6Hz||
|Galaga|20180313|240p|15.86kHz, 60.6Hz||
|Galaxian|20180313|240p|15.86kHz, 60.6Hz||
|GalaxyWars|20171115|VGA|37.8kHz, 60.3Hz||
|Gorkans|20180313|240p|15.86kHz, 60.6Hz||
|Invaders|20181010|VGA|31.20kHz, 59.9Hz||
|Joust|20181216|240p|15.49kHz, 60.0Hz||
|LadyBug|20180313|240p|15.49kHz, 60.0Hz||
|LizardWizard|20180313|240p|15.49kHz, 60.0Hz||
|LodeRunner|20171115|VGA|37.8kHz, 60.3Hz||
|LunarRescue|20171115|VGA|37.8kHz, 60.3Hz||
|Mayday|20181218|240p|15.49kHz, 60.0Hz||
|MoonCresta|20180313|240p|15.49kHz, 60.0Hz||
|MoonPatrol|20180315|240p|15.51kHz, 50.0Hz||
|MrDoNightmare|20180313|240p|15.49kHz, 59.1Hz||
|MrTNT|20180313|240p|15.49kHz, 59.1Hz||
|MsPacman|20180313|240p|15.49kHz, 59.1Hz||
|Omega|20180313|240p|15.49kHz, 59.1Hz||
|Orbitron|20180313|240p|15.49kHz, 59.1Hz||
|Pacman|20180313|240p|15.49kHz, 59.1Hz||
|PacmanClub|20180313|240p|15.49kHz, 59.1Hz||
|PacmanPlus|20180313|240p|15.49kHz, 59.1Hz||
|PacmanicMiner|20180313|240p|15.49kHz, 59.1Hz||
|Pengo|20180313|240p|15.49kHz, 59.1Hz||
|Phoenix|20180313|240p|15.49kHz, 59.1Hz||
|Pisces|20180313|240p|15.49kHz, 59.1Hz||
|Ponpoko|20180313|240p|15.49kHz, 59.1Hz||
|Pooyan|20180313|240p|15.49kHz, 59.1Hz||
|Robotron|20181215|240p|15.49kHz, 59.1Hz||
|Scramble|20180929|240p|15.86kHz, 60.6Hz||
|Sinistar|20181218|240p|15.86kHz, 60.6Hz||
|SnapJack|20180315|240p|15.86kHz, 60.6Hz||
|Space Attack II|20171115|VGA|37.8kHz, 60.3Hz||
|Space Invaders|20171115|VGA|37.8kHz, 60.3Hz||
|Space Invaders Part II|20171115|VGA|37.8kHz, 60.3Hz||
|Space Laser|20171115|VGA|37.8kHz, 60.3Hz||
|Splat|20181217|240p|15.86kHz, 60.6Hz||
|Stargate|20181216|240p|15.86kHz, 60.6Hz||
|Super Earth Invasion|20171115|VGA|37.8kHz, 60.3Hz||
|SuperGlob|20180313|240p|15.86kHz, 60.6Hz||
|TheEnd|20180313|240p|15.86kHz, 60.6Hz||
|TimePilot|20180313|240p|15.86kHz, 60.6Hz||
|VanVanCar|20180313|240p|15.86kHz, 60.6Hz||
|WarOfTheBugs|20180103|240p|15.86kHz, 60.6Hz||
|Woodpecker|20180313|240p|15.86kHz, 60.6Hz||
|Xevious|20180313|240p|15.86kHz, 60.6Hz||
|ZigZag|20181219|240p|15.86kHz, 60.6Hz||
