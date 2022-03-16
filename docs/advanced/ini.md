The [MiSTer.ini configuration file](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini){target=_blank} contains global settings and is capable of storing core-specific settings for the MiSTer. We'll go over each of the Global settings here and then show you how to make exceptions for those global settings for each core. Then we'll describe some core-specific settings that can be used for core exceptions only.

## General Video Settings 

`vscale_mode` - Changes how the image is scaled to the screen. 0 will fit the whole image to screen, 1 is 1:1 integer scaled, 2 uses 0.5 steps to scale, and 3 uses 0.25 steps to scale.

`vscale_border` - Sets an overscan border to the screen in number of pixels (1-399)

`hdmi_limited` - Changes the color range output over HDMI. 0 = `0-255`, 1 = `16-235`, and 2 = `16-255`. A setting of 2 can be useful if you have problems with some Digital Video adapters. It can also help if your screen has a dynamic backlight and you want to brighten things up, to change the setting to 1.

`fb_size` - Effects the scaling of things drawn to the Linux framebuffer, such as when you run scripts. Best left to 0 for automatic.

`video_mode` - Sets the resolution for HDMI and VGA_Scaler output. This can be one of the premade values from 0-13 or it can be a custom video mode. See the notes in the [.ini Master](https://github.com/MiSTer-devel/Main_MiSTer/blob/2b0b8a1422540fa5c49e6a71a694848143341c87/MiSTer.ini#L75){target=_blank} for custom video mode syntax. There is also a useful custom video mode tool by morf77 [available here](https://morf77.pythonanywhere.com/){target=_blank} which can be used in conjunction with a [modeline calculator](https://arachnoid.com/modelines/){target=_blank}.

`video_info` - Number of seconds that it will display the video info in the top left corner of the screen whenever the resolution or frequency has changed.

`vsync_adjust` - Adjusts the buffer settings for the frames sent to the display. For more details on how this works, see the [Video Configuration](../basics/video.md#vsync_adjust){target=_blank}'s vsync_adjust section. Essentially, the values of `0-2` are in order of most compatible+highest lag to least compatible+lowest lag.

`refresh_min` - Forces a minimum refresh rate.

`refresh_max` - Forces a maximum refresh rate.

`` - 

## Analog Video Settings

`forced_scandoubler` - VGA output will always run in 31kHz mode (scandoubled) if this setting is turned on, useful for computer CRT's.

`ypbpr` - Changes the VGA output to a YPbPr signal.

`composite_sync` - Sends the sync signal on Hsync over VGA output, needed for certain configurations.

`vga_scaler` - Sends the scaler output to the VGA port (either Analog IO or Direct Video). This is usually used with computer CRTs and other 31kHz displays which are not compatible with 240p TV signals.

`menu_pal` - Forces the Menu core to run in PAL mode.

`direct_video` - This changes the HDMI output to an analog signal, only supported with certain Direct Video Adapters that have AG62xx chipsets. If you have issues with color or no image, in addition to checking `composite_sync` and `ypbpr` options, you can also try changing `hdmi_limited` to `1`. If you are using `ypbpr` with component cables, the Direct Video adapter will need a modification to combine HSYNC and Green in order to work.

`fb_terminal` - Best left at 1. If you have issues with running scripts on a CRT or Analog display, try switching this to 0 to see if that helps.

## Audio Settings

`hdmi_audio_96k` - Changes the HDMI audio sampling rate from 48kHz (default) to 96kHz. This can help with the audio of some systems that have strange sampling rates (like Turbografx-16's sampling rate of 32.088kHz for instance).

`dvi_mode` - DVI mode over the HDMI connection, this disables audio transmission over HDMI when turned on.

## Controller Settings

`mouse_throttle` - Can be used to change the speed of your mouse (1-100). Good for very sensitive mice.

`gamepad_defaults` - 

`bt_auto_disconnect` - Amount of minutes of inactivity before Bluetooth disconnects automatically. Default is 0 (off).

`bt_reset_before_pair` - Resets bluetooth adapter before pairing dialog. If you enable this some input devices may get shutdown after a reset.

## Menu Settings

`rbf_hide_datecode` - Hides the date codes from the core names in the core selection menu.

`osd_timeout` - The length of time the OSD is displayed when brought up and no inputs have been pressed. 0 - never timeout, and the range of values are 5-3600 seconds.

`osd_rotate` - Rotate the OSD. Useful for when you rotate your monitor for certain Arcade cores. 0 - no rotation, 1 - rotate right (+90°), and 2 - rotate left (-90°).

## Debug Settings

`log_file_entry` - Writes filename under the curse in browser for use by external integrations.
