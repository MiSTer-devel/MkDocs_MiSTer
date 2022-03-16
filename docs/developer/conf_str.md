---
hide:
  - toc
---

MiSTer provides an on-screen display (OSD) that can be toggled on and off by pressing F12 on your keyboard (or OSD button). For each core that is loaded, this menu can be configured to add specific options for that core.

The top-level module for the cores is `emu`. This does **NOT** mean `emu` is the top-level module for the project, but rather it is the top-level module for our purposes. The `emu` module is typically found in the SystemVerilog file (`*.sv` extension) with the same name as the project. As an example, the Arcade-Galaga project has it's top-level module at `Arcade-Galaga.sv`.

The configuration string is stored in the variable `CONF_STR` of the `emu` module. This variable is passed to the `hps_io` module that handles sending it to the processor to be read when necessary.

Each line of the configuration string is delimited with a semicolon.

Most cores have a Status Bit Map placed at the top of the `CONF_STR` section. When developing a core, please use this as it's a helpful reference which aids in collaboration. This reference is edited by fellow developers to communicate which status bits are occupied. Only one option can occupy `status[8]` so this is important.

## Status Bit Map

For example with nothing occupied:

```
// Status Bit Map:
//             Upper                             Lower              
// 0         1         2         3          4         5         6   
// 01234567890123456789012345678901 23456789012345678901234567890123
// 0123456789ABCDEFGHIJKLMNOPQRSTUV 0123456789ABCDEFGHIJKLMNOPQRSTUV
// 
```

If you add a status bit option like `O89` to the core configuration string, this is going to use the first group of status bits on the left since the "O" for option is capitalized (marked Upper). Then it's going to use 8 and 9, this is from the bottom row (which is alphanumeric). So you would update the index after using these like so:

```
// Status Bit Map:
//             Upper                             Lower              
// 0         1         2         3          4         5         6   
// 01234567890123456789012345678901 23456789012345678901234567890123
// 0123456789ABCDEFGHIJKLMNOPQRSTUV 0123456789ABCDEFGHIJKLMNOPQRSTUV
//         XX
```

This will communicate to other developers that `status[9:8]` are occupied and should not be used.

## Valid options for the menu

`[]` - means optional parameter

* `C[,{Text}]` - Enables a cheat menu entry with the label `{Text}`.
* `CHEAT` - like DIP, for arcades with a cheat system
* `D{Index}` - Prefix which disables the option if `menumask[Index]` is set.
* `d{Index}` - Same as 'D', but disables the option if `menumask[Index]` is NOT set.
* `DIP` - in arcade cores, this will display the DIP menu from the MRA
* `F[S][#],{Ext}[,{Text}][,{Address}]` - Load file button. 
  * `{Ext}` - a concatenated list of 3 character file extensions. For example, `BINGEN` would be `BIN` and `GEN` extensions.
  * Optional `{Text}` string is the text that is displayed before the extensions like "Load RAM". If `{Text}` is not specified, then default is "Load \*".
  * Optional `[S]` - core supports save files, load a file, and mount a save for reading or writing
  * `#` is explicit index (or index is generated from line number if index not given).
  * Optional `{Address}` - load file directly into DDRAM at this address
  * ioctl_index from hps_io will be: ioctl_index[5:0] = index(explicit or auto), ioctl_index[7:6] = extension index
* `FC[#],{Ext}[,{Text}][,{Address}]` - Open file and remember it, useful for remembering an alternative rom, config, or other type of file. See F for how the options work.

* `H{Index}` - Prefix which hides the option if `menumask[Index]` is set.
* `h{Index}` - Same as `H`, but hides the option if `menumask[Index]` is NOT set.
* `O{Index1}[{Index2}],{Name},{Options...}` - Option button that allows you to select between various choices.
  * `{Index1}` and `{Index2}` are values from 0-9 and A-V (like Hex but it extends from A-V instead of A-F). This represents all 31 bits. First and second index are the range of bits that will be set in the status register.
  * `{Name}` is what is shown to describe the option.
  * `{Options...}` - a list of comma separated options.
* `P{#},{Title}` - Creates sub-page for options with `{Title}`.
* `P{#}` - Prefix to place the option into specific `{#}` page. This is added before `O#` but after something like `d#`. (e.g. `"d5P1o2,Vertical Crop,Disabled,216p(5x);",` is correct and `"P1d5o2,Vertical Crop,Disabled,216p(5x);",` is incorrect and the menu options will not work.)
* `R{Index},{Name}` - Same as T option but closes the OSD after selecting. Convenient for Reset option.
* `S{Slot},{Ext}[,{Text}]` - Mount SD card button. 
  * `{Slot}` - a value from 0-3. Up to four images can be mounted at the same time.
  * `{Ext}` - same as in `F` option.
  * (Optional) `{Text}` - The text that is displayed before the extensions like "Load RAM". If `{Text}` is not specified, then default is "Mount \*".
* `T{Index},{Name}` - Trigger button. This is a simple button that will pulse HIGH of specified `{Index}` bit in status register. A perfect example of this is for a reset button.
  * `{Name}` is the text that describes the button function.
* `-[,TEXT]` - empty (or with `TEXT`) line.
* Lower case options `o`,`t`,`r` equal their upper case variants with adding 32 to status bit indexes.

## Non-OSD options

These must be placed at the bottom of the configuration string:

* `J[1],{Button1}[,{Button2},...]` - J1 means lock keyboard to joystick emulation mode. Useful for keyboard-less systems such as consoles. {Button1},{Button2},... is list of joystick buttons used in the core. Up to 12 buttons can be listed. Analog axis are not defined here. The user just needs to map them through the Menu core.
* `jn,{SNES Button Name1},[,{SNES Button2},...]` - this sets the default mapping of the buttons. ie: jn,A would map joystick bit 4 to the A button on a SNES style controller automatically
* `jp` - same as `jn` but used when `gamepad_defaults=1` in `MiSTer.INI`. Typically refers to positional mapping relative to a SNES controller
* `V,{Version String}` - Version string. {Version String} is the version string. Takes the core name and appends version string for name to display.
* `I,INFO1,INFO2,...,INFO255` - `INFO1-INFO255` lines to display as OSD info (top left corner of screen).
* `DEFMRA,{mra name}` - default MRA (ie: Puckman.mra) to be used when core is uploaded by USB blaster (debug)

## jn vs. jp and mapping conventions

* jn mapping is the default.
* jp mapping is used when the INI file has gamepad_defaults=1
* the only difference in the two mappings is the "philosophy" of how they are expected to work

The difference is one of convention when mapping buttons:
* jn is name-base mapping 
* jp is position-based mapping

**What does this mean?**

Consider how the internal gamepad is defined on MiSTer:

1. Internally, controllers are mapped in the menu core to a SNES-style gamepad 
2. The button order on the internal MiSTer gamepad is ABXYLR + Start + Select
3. That is: button 1=A, button 2=B, and so on.

With "jn" mapping:
* the convention is to map button A of the core to the internal "SNES A" button.
* If the core has no button "A", this would be the first button. 
* Second button would be "SNES B", and so forth.
* This is because the name or order of the button matches the original definition (ABYXLR etc)

With "jp" mapping:
* the convention is to consider the physical location of each button
* For a Genesis 3-button controller that has A, B, C as buttons, mapping would be "SNES Y, SNES B, SNES A"
* This is because YBA on a SNES gamepad are the lower 3 buttons of the controller
