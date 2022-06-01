The [MiSTer TurboGrafx16 core](https://github.com/MiSTer-devel/TurboGrafx16_MiSTer){target=_blank} is an extremely accurate TurboGrafx 16 / PC-Engine hardware based emulator. Originally based upon [Gregory "Torlus" Estrade's FPGAPCE](https://github.com/Torlus/FPGAPCE){target=_blank}, it has been pushed even further to a high degree of accuracy by the best MiSTer devs and PC-Engine experts. The MiSTer TurboGrafx16 core has support for SuperGrafx, CD-ROM, and Arcade Cards.

## Controller Options

In the OSD you are able to change the intended simulation of the controller you are using in various ways. For Pachio-Kun there was a pachinko style controller which had an angled slider to adjust the angle of the pachinko balls in-game. You can use a mouse for this movement instead.

The Turbo Tap controller is also supported. This is distinct from the MiSTer's built-in Turbo feature. The Turbo Tap had a specific turbo frequency that is more suitable for some games. Enablingt his option will make the buttons use turbo at the original rate of that controller.

There is also a toggle so you can change to the rarely used PC-Engine 6-button controller. There was a controller called the "HORI Fighting Commander PC" and a couple other controllers with this I - VI button scheme and turbo tap functionality on each of them. This 6-button controller was only supported on a select few games. Here's a list of these 6-button supported games:

* Advanced Variable Geo
* Art of Fighting
* Asuka 120% Maxima Burning Fest
* Fatal Fury 2
* Fatal Fury Special
* Flash Hiders
* Flash Hiders Taikenban (Demo)
* Kabuki Klash
* World Heroes II
* Ys IV - Dawn of Ys

## Arcade card

There are a few TurboGrafx16 games which required the Arcade card add-on. The MiSTer core supports running these, all you have to do is toggle the "Arcade Card" option to "Enabled" in the "Hardware" sub-menu, then it should work.

## Color palette options

The composite video encoder of the original TurboGrafx-16 modified the colors from their raw RGB values. What this means is, how you saw the colors on real hardware on an old CRT years ago, is not how it looked in emulators today or even RGB-modded original hardware! Thankfully Kitrinx and Artemio Urbina worked to develop a [mathematically derived color corrected palette](https://www.retrorgb.com/pc-engine-palette-improvements-the-amazing-people-behind-the-technology.html){target=_blank} that represents the composite video output instead. The games were likely developed with these composite colors in mind, so this option is kept as the default. If you want a more vibrant color with a lot of pop, then you can switch to the Raw RGB setting instead by toggling the Audio & Video --> Colors option. Here's a video demonstrating how to change this option and the big difference it makes:

![type:video](videos/tgfx16-palette.mp4)

## Overscan / Border and Border Color

The original TurboGrafx-16 had a border that was mostly not visible to the original player due to the bezel of their CRT covering this empty space. In the MiSTer TGFX16 core we leave this overscan area hidden to make it more pleasant on modern displays. If you wish to restore this overscan and if you wish to use the original system's color (instead of just Black) for it, you can just change the Overscan and Border Color options.

## Extra Sprites per Line

The original TurboGrafx-16 hardware had a hard limit to how many sprites could be rendered per line at a time, so when a game went over this limit they would flicker and disappear to compensate. The MiSTer core isn't forced to adhere to these limitations. While the default behavior is the same as the hardware you can turn this option to "Extra" in the OSD's Audio & Video sub-menu and see if it makes the game more pleasant. Here's a video example:

![type:video](videos/tgfx16-flicker.mp4)

## Audio Boost options

Some games had varying levels of audio when compared to each other, and even to their own separate audio channels. The MiSTer TurboGrafx16 core allows you to Boost the CD Audio, ADPCM, and all Audio by varying degrees. This can help when the vocals are quieter than the music, or when some sound effects feel like they should be louder, or even if a game is randomly just a lot quieter on the whole than the other games you were just playing.

