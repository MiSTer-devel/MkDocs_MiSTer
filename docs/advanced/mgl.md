---
hide:
  - toc
---

MGL files are a new way to load ROMs directly from the Menu core. This feature could potentially change more in the future as it's very new.

## MGL files run games automatically

You can add your favorite games to the main menu (below the Arcade, Computer, Console etc. folders) - or - e.g. inside a folder for instance called 'Favorites'. It needs to be named _Favorites in the file system to show up in the menu.

Each of your favorite games must have an MGL file to be accessible in the menu.

At the time of writing (late February 2022) MGL is not supported on the Atari ST, Minimig, Archie and Sharp cores.

## MGL Format

Examples:

```xml
<mistergamedescription>
	<rbf>_console/snes</rbf>
	<file delay="2" type="f" index="0" path="dummy.snes"/>
</mistergamedescription>
```

```xml
<mistergamedescription>
	<rbf>_console/gameboy</rbf>
	<file delay="1" type="f" index="1" path="dummy.gbc"/>
</mistergamedescription>
```

```xml
<mistergamedescription>
	<rbf>_Computer/C64</rbf>
	<file delay="1" type="f" index="1" path="dummy.prg"/>
</mistergamedescription>
```

* `<rbf>`: path to the core and its name. If the core is outside the _console folder just its name.
* `<file delay=` amount of seconds to wait before load/mount (e.g. 1:turbografx16, neogeo, gba, gameboy, genesis, c64 and 2:snes).
* `type=` f: load file. s: mount
* `index=` 0 for most console cores but 1 for e.g. the NeoGeo and Gameboy cores.
* `path=` path to game file inside the core's games folder. E.g. Puzzles/Dummy.bin

All parameters must be present.

If a core pops up the OSD menu after loading the game or the game doesn't load try increasing the delay. It could also be due to wrong the index number, file type or game file path so check those too.

Until a complete **list of cores and their index numbers and file types** is ready you can test different index numbers and the file types listed above or look at the code for each core on Github. 

E.g. for the **TurboGraphics** core you can take a look at the file **TurboGrafx16.sv** to see the index numbers and file types supported by that core. Find a section that starts with `parameter CONF_STR` and in that section look for the ROM type you are loading/mounting. In this case it will be `"S0,CUECHD,Insert CD;"`. Notice the S0, that is the "s" type with index of 0.
