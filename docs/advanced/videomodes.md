The `#!ini video_mode` INI setting supports several different methods of specifying the video mode.


## Automatic Detection
If no `#!ini video_mode` setting is specified, MiSTer will attempt to determine the correct video mode using EDID information from the display device. This will only work for devices connected to the HDMI port. If a valid video mode cannot be determined then the default 720p mode will be used.


## Presets
MiSTer has 15 built in video mode presets ranging from 0-14. These presets cover a lot of common display modes used by televisions and computer monitors. Here's an example video_mode setting and a table below to explain what each of the preset modes are:
```ini
; Number 8 - 1920x1080 - 60hz - 16:9 - FHD 1080p
video_mode=8
```

| Number | Resolution | Refresh (Hz) | Aspect Ratio | Name          |
| ------ | ---------- | ------------ | ------------ | ------------- |
| 0      | 1280x720   | 60           | 16:9         | HD 720p       |
| 1      | 1024x768   | 60           | 4:3          | XGA           |
| 2      | 720x480    | 60           | 3:2          |               |
| 3      | 720x576    | 50           | 5:4          |               |
| 4      | 1280x1024  | 60           | 5:4          | SXGA          |
| 5      | 800x600    | 60           | 4:3          | SVGA          |
| 6      | 640x480    | 60           | 4:3          | VGA           |
| 7      | 1280x720   | 50           | 16:9         | HD 720p PAL   |
| 8      | 1920x1080  | 60           | 16:9         | FHD 1080p     |
| 9      | 1920x1080  | 50           | 16:9         | FHD 1080p PAL |
| 10     | 1366x768   | 60           | 16:9         | WXGA          |
| 11     | 1024x600   | 60           | 128:75       | WSVGA         |
| 12     | 1920x1440  | 60           | 4:3          |               |
| 13     | 2048x1536  | 60           | 4:3          | iPad Retina   |
| 14     | 2560x1440  | 60           | 16:9         | 1440p         |


## Custom Modes
A custom mode can be set by specifying the width, height and refresh rate like so:
```ini
; 1920x1200 at 75Hz
video_mode=1920,1200,75
```
The maximum value for width is 4096, height is 2048 and refresh rate is unlimited but it must be a whole integer value. The DE-10 may not be able to output the mode you select or your display may not be able to accept it. The maximum recommended video frequency is 210Mhz which limits the maximum resolution to 2048x1536. [Pixel repetition](#hdmi-pixel-repetition) can be used to increase the resolution further, but it also has limits.

The VESA [Coordinated Video Timings](https://en.wikipedia.org/wiki/Coordinated_Video_Timings){target=_blank} standard is used to calculate the timing information for the requested video mode. By default the reduced blanking version of the standard is used. This is compatible with most flat panel displays but may not be as well supported on older displays and CRT monitors. You can use regular CVT timings by adding the `#!ini cvt` flag to the end of the video mode:
```ini
; 1600x1200 on a CRT monitor
video_mode=1600,1200,60,cvt
```
Regular timing requires a slightly higher clock speed for a given resolution, so it some higher resolution modes are not achievable with it. An [online video timing calculator](https://tomverbeure.github.io/video_timings_calculator){target=_blank} can help with understanding the differences between the two methods.


## Modelines
Video mode timing can be fully specified using a video modeline which consists of nine values defining the horizontal timing, vertical timing and pixel clock.
```ini
video_mode=hact,hfp,hs,hbp,vact,vfp,vs,vbp,fpix
```
`#!ini hact` and `#!ini vact` defines the active (visible) size of the video mode in horizontal and vertical pixels, respectively. `#!ini hfp`, `#!ini hs` and `#!ini hbp` defines the duration of horizontal front porch, sync and back porch in pixels. `#!ini vfp`, `#!ini vs` abd `#!ini vbp` define the same properties, but for the vertical timing. Finally, the `#!ini fpix` value is the frequency of the pixel clock in KHz (pixels clocks are usually specified in MHz, so multiply the Mhz value by a 1000 to get the value in KHz).

MiSTer modelines are similar to XFree86 modelines, but the information is expressed slightly differently. You can convert an XFree86 modeline to a MiSTer one using the custom video mode tool by morf77 [available here](https://morf77.pythonanywhere.com/){target=_blank} which can be used in conjunction with a [modeline calculator](https://arachnoid.com/modelines/){target=_blank}.


## Additional Flags
Some additional flags can be added to custom modes and modelines to modify the behavior.

 * `#!ini +hsync` / `#!ini -hsync` - set the horizontal sync polarity
 * `#!ini +vsync` / `#!ini -hsync` - set the vertical sync polarity
 * `#!ini pr` - use HDMI pixel repetition (custom modelines only)
 * `#!ini cvt` - use normal CVT timing (custom mode only)
 * `#!ini cvtrb` - use reduced blanking CVT timing (custom mode only)


## HDMI Pixel Repetition
HDMI pixel repetition enables MiSTer to output a higher resolution video signal without using additional resources or requiring higher clock speeds. It does this by instructing the ADV7513 HDMI transmitter to duplicate each pixel that it sends to the display. This does not increase the fidelity of the final image, in most cases it will reduce it, but it does enable a wider selection of video modes.

MiSTer is limited to a maximum horizontal resolution of 2048 pixels and a maximum pixel clock of 210Mhz. This is enough to display a 2048x1536 image (209Mhz, Pad resolution), which is the maximum native resolution supported. It is also enough for 1920x1440 (184Mhz) which is a non-standard 4:3 resolution supported by some displays. The more commonly supported 2560x1440 mode is out of reach both because of its large horizontal resolution and because of its 240Mhz pixel clock.

Pixel repetition makes a mode like 2560x1440 possible by lowering the horizontal resolution to 1280 pixels which lowers the pixel clock to 120Mhz. The 1280x1440 image that the MiSTer scaler produces is stretched horizontally by the ADV7513 so the signal that the display receives is the full 2560x1440.

![Pixel Repetition Pipeline](img/pixel-repeat.png)

An update to the framework is required to support the non-uniform scaling for the cores output and pixel repetition is only supported for cores that have been updated. Older cores will have their output set to 1920x1080 if a mode requiring pixel repetition is requested.
