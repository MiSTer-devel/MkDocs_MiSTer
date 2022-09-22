MGL files are used as a custom method to load games directly from the MiSTer FPGA's Menu core.

They can be placed in the root of the SD card to show up in the top of the menu, or in a menu folder. A menu folder is a regular folder with an underscore (`_`) in front that will display in the menu. You can create your own menu folders.

Not all cores support MGL files, though all the most popular cores do. Console support is good, but computer cores generally don't work well with them.

## MGL Format

MGLs are simple XML files with the file extension `.mgl`. Whatever name you give to an MGL file (excluding the extension) is what will be shown for its entry in the menu. E.g. `My Favorite Game.mgl` will display in the menu as `My Favorite Game`.

Example MGL files:

```xml
<mistergamedescription>
	<rbf>_console/snes</rbf>
	<file delay="2" type="f" index="0" path="puzzles/dummy.sfc"/>
</mistergamedescription>
```

```xml
<mistergamedescription>
	<rbf>_console/psx</rbf>
	<file delay="1" type="s" index="0" path="dummy.chd"/>
</mistergamedescription>
```

```xml
<mistergamedescription>
	<rbf>_Computer/C64</rbf>
	<file delay="1" type="f" index="1" path="some/other.zip/path/dummy.prg"/>
</mistergamedescription>
```

```xml
<mistergamedescription>
	<rbf>_Console/SMS</rbf>
	<setname>GameGear</setname>
	<file delay="1" type="f" index="2" path="dummy.gg"/>
</mistergamedescription>
```

* `rbf`: Relative path to the core's RBF file from the SD root, excluding its file extension and timestamp.
* `setname`: Sets a core's name to this value, changing its games folder and config file.
* `file`: The file to be loaded into the core and its launch arguments.
  * `delay` Amount of seconds to wait before load/mount.
  * `type` Either `f` for load file to memory or `s` for mount file.
  * `index` Pointer to slot where file is loaded in core.
  * `path` Path to game file relative to the core's games folder.

The `rbf` and `file` tags must be present.

The `setname` tag is optional. It will make a core temporarily point to a different games folder and config file. Useful for cores which play multiple systems, or often need to toggle between different configurations.

The `type` and `index` attributes depend on what values were configured by the core's developer. See below for [how to check those](#finding-mgl-arguments).

If a core pops up the OSD menu after loading the game or the game doesn't load, try increasing the `delay` value.

## MGL Arguments

Some MGL arguments for common cores:

| System              | RBF                   | Delay | Index   | Type |
| ------------------- | --------------------- | :---: | :-----: | :--: |
| Atari 2600/7800     | _Console/Atari7800    | 1     | 1       | f    |
| Atari 5200          | _Console/Atari5200    | 1     | 0       | s    |
| Atari Lynx          | _Console/AtariLynx    | 1     | 0       | f    |
| Commodore 64        | _Computer/C64         | 1     | 1       | f    |
| Famicom Disk System | _Console/NES          | 1     | 0       | f    |
| Game Boy (Color)    | _Console/Gameboy      | 1     | 1       | f    |
| Game Boy Advance    | _Console/GBA          | 1     | 0       | f    |
| Game Gear           | _Console/SMS          | 1     | 2       | f    |
| Genesis             | _Console/Genesis      | 1     | 0       | f    |
| Master System       | _Console/SMS          | 1     | 1       | f    |
| Sega CD             | _Console/MegaCD       | 1     | 0       | s    |
| Neo Geo             | _Console/NeoGeo       | 1     | 1       | f    |
| NES                 | _Console/NES          | 1     | 0       | f    |
| Playstation         | _Console/PSX          | 1     | 1       | s    |
| Sega 32X            | _Console/S32X         | 1     | 1       | f    |
| SNES                | _Console/SNES         | 2     | 0       | f    |
| TurboGrafx-16       | _Console/TurboGrafx16 | 1     | 0       | f    |
| TurboGrafx-16 CD    | _Console/TurboGrafx16 | 1     | 0       | s    |

A more comprehensive list of MGL argments can be found [here](https://github.com/wizzomafizzo/mrext/blob/main/docs/systems.md).

## Arcade Cores

Arcade cores cannot be launched using MGL files. If you want to make a shortcut to an arcade core elsewhere in the menu, you'll instead have to *symlink* it there.

For example, either through SSH or the console (press `F9` from the menu):
```
# ln -s /media/fat/_Arcade/dummy.mra /media/fat
# ln -s /media/fat/_Arcade/cores /media/fat
```

This would make a shortcut to an arcade core in the root of the MiSTer menu. It can also be done with menu subfolders.

Take note of the second line, symlinking the `cores` folder. You have to do this once for each folder you want to symlink MRA files into.

## Finding MGL Arguments

If the core you are looking for isn't in these lists, you can either test out the combinations yourself, or you can look at the code on GitHub for the core to figure out the values directly.

For example, to get the values for the **TurboGrafx-16**, core you can take a look at the file [TurboGrafx16.sv](https://github.com/MiSTer-devel/TurboGrafx16_MiSTer/blob/master/TurboGrafx16.sv){target=_blank} on GitHub to find the index numbers and file types supported by that core. First find the section that starts with `parameter CONF_STR` and in that section look for the file type you are launching. In this case it will be `"S0,CUECHD,Insert CD;"`. Notice the S0, that is the "s" type with index of 0.

See the [Core Configuration String](../developer/conf_str.md) page for detailed information on this format.
