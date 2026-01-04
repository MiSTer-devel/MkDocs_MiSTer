The Sega Saturn MiSTer core, developed originally by [srg320 (Sergey Dvodnenko)](https://www.patreon.com/srg320/){target=_blank}, provides a suitable modern replacement to original hardware in the vast majority of games in the Sega Saturn library.

## Controller/Accessories Support

- USB/Bluetooth:

    - Supports (maximum 2 controllers):

        - Control Pad (the default controller)
        - Mouse
        - Lightguns
 
    - Missing:

        - Full 3D Control Pad support [^1]
        - Twin-Stick
        - MIDI
        - Keyboard + FDD Operator
        - Video Card
        - NetLink
        - Floppy Disk Drive
        - Keyboard

- [SNAC](./../../basics/input.md#serial-native-accessory-convertor-snac): 
    - Supported:

        - Control Pad
        - 3D Pad
        - Virtua Gun (aka _Stunner_)
        - Twin-Stick (with Cyber Troopers Virtual-On)
        - Shuttle Mouse

    - Not currently supported:

        - Saturn MIDI Interface Box

    - To be confirmed:

        - Multitap (via SNAC)

## Media support

  - Multi-disc support
  - CHD support
  - Multiple region support + Automatic region detection

## BIOS and region selection

### TL;DR

The best user experience is with a region-free BIOS if you have one.

By placing a BIOS as `boot.rom` in the `games/Saturn` folder, the core will auto-load it when starting.

### Multiple BIOS

If wanting to use multiple BIOS and/or control which are used per games (automatically when opening the core), place them named as `cd_bios.rom` in either:

- the same folder as the game
- a parent folder of the game (e.g. a folder for Japanese released games with the Japanese Saturn BIOS, with the games in subfolders there).

### Other

The OSD menu of the core also allows:

- manual loading of BIOS (when named with a `*.bin` extension)
- setting automatic region detection.

## Options

We do not cover all options, but document a key one.

### "Fast timings"

After loading the core, in the OSD, under `Hardware -> Timings` you will find an option to set timings to:

- `Normal` (default)
- `Fast` (commonly referred to as "fast timings")

Whilst `Fast` is made available, it can break some titles (e.g. freezes and graphical glitches) and is best not used as default[^2]. It exists to address issues in the `Normal` mode with the released version of the core.

## FAQ

### Dual SDRAM vs Single SDRAM builds

MiSTer systems are expected to have a single 128MB SDRAM module. Official core releases only target a single module at most.

As part of their development workflow, developers can start with two SDRAM modules in their development hardware (at the expense of losing some analogue functionality) simply for development convenience. This is to obtain extra bandwidth before the core is optimised for official releases targetting the single SDRAM builds of end users. 

During development and/or before cores reach that stage, or as the limit of the hardware is reached, Dual SDRAM variants of cores might be distributed unofficially in the community. Some enthusiasts also build SDRAM stacks while using experimental builds.

In the Saturn core, the Dual SDRAM builds continue to be built and discussed due to a few outstanding but generally minor issues present in the official single SDRAM build. A number of these can currently be mitigated with the [fast timings](#fast-timings) option, but not all. Releases are not official and use of single SDRAM builds continues to be encouraged.

More info [here](https://github.com/MiSTer-devel/Saturn_MiSTer/issues/251#issuecomment-2482401756){target=_blank} from the developer.

## Known issues

Please review the rest of this page as we document limitations per feature/section.

The remaining [GitHub issues](https://github.com/MiSTer-devel/Saturn_MiSTer){target=_blank} covers these more thoroughly[^3].

## Source code

Available [here](https://github.com/MiSTer-devel/Saturn_MiSTer){target=_blank}.


[^1]: Analogue triggers (to replicate the 3D Control Pad) are not currently supported. If set to use the 3D Control Pad, the core will simply not feed input to the triggers (e.g. to map digital to analogue signal, or use the compatibility digital mode of the 3D Control Pad, as that is equivalent to the Control Pad mode already supported)
[^2]: see these comments: [1](https://github.com/MiSTer-devel/Saturn_MiSTer/issues/251#issuecomment-2481394472){target=_blank}, [2](https://github.com/MiSTer-devel/Saturn_MiSTer/issues/251#issuecomment-2481418725){target=_blank}
[^3]: some issues may be out of date and no longer apply (and/or require more testing before closing)