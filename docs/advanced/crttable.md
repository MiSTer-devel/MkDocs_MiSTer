---
hide:
  - toc
---

Here's a table that shows you what options correlate to what video connection, to make it a bit easier to decide what you need in order to connect to your CRT, and what settings are required in the MiSTer.ini to get it to work. There is also a physical switch on the Analog IO board, in this table it is referred to as "SoG Switch".

## CRT Configuration Table

| Analog Video Out     | composite_sync= | vga_mode= | vga_sog= | direct_video= | vga_scaler= | forced_scandoubler= | SoG Switch |
| -------------------- | :-------------: | :-------: | :------: | :-----------: | :---------: | :-----------------: | :--------: |
| RGBS Native          | 1               | rgb       | 0        | 0             | 0           | 0                   | AUTO       |
| RGBS Scan-doubled¹   | 1               | rgb       | 0        | 0             | 0           | 1                   | AUTO       |
| RGBS Upscaled²       | 1               | rgb       | 0        | 0             | 1           | 0                   | AUTO       |
| RGBS Direct³         | 1               | rgb       | 0        | 1             | 0           | 0                   | N/A        |
| RGBHV Native         | 0               | rgb       | 0        | 0             | 0           | 0                   | AUTO       |
| RGBHV Scan-doubled   | 0               | rgb       | 0        | 0             | 0           | 1                   | AUTO       |
| RGBHV Upscaled²      | 0               | rgb       | 0        | 0             | 1           | 0                   | AUTO       |
| RGBHV Direct³        | 0               | rgb       | 0        | 1             | 0           | 0                   | N/A        |
| RGsB Native          | 1               | rgb       | 1        | 0             | 0           | 0                   | AUTO       |
| RGsB Scan-doubled¹   | 1               | rgb       | 1        | 0             | 0           | 1                   | AUTO       |
| RGsB Upscaled²       | 1               | rgb       | 1        | 0             | 1           | 0                   | AUTO       |
| RGsB Direct³         | 1               | rgb       | 1        | 1             | 0           | 0                   | N/A        |
| YPbPr Native         | 0               | ypbpr     | 1        | 0             | 0           | 0                   | OVR        |
| YPbPr Scan-doubled   | 0               | ypbpr     | 1        | 0             | 0           | 1                   | OVR        |
| YPbPr Upscaled²      | 0               | ypbpr     | 1        | 0             | 1           | 0                   | OVR        |
| YPbPr Direct³⁴       | 0               | ypbpr     | 0        | 1             | 0           | 0                   | N/A        |
| S-Video Native⁵      | 1               | svideo    | 0        | 0             | 0           | 0                   | N/A        |
| S-Video Converted⁶   | 1               | rgb       | 0        | 0             | 0           | 0                   | N/A        |
| Composite Native⁵    | 1               | svideo    | 0        | 0             | 0           | 0                   | N/A        |
| Composite Converted⁶ | 1               | rgb       | 0        | 0             | 0           | 0                   | N/A        |

¹ Scan-doubled = 2x resolution (e.g. 240p > 480p)  
² Upscaled resolution = video_mode  
³ External "direct video" (HDMI to VGA) adapter required - native resolution only (no upscaling or scan-doubling  
⁴ External "direct video" adapter requires modification to pass Sync on Green (SoG)  
⁵ Active Y/C converter required  
⁶ External RGB to NTSC/PAL converter required
 
Credit: [Porkchop Express](https://twitter.com/MisterAddons){target=_blank}
