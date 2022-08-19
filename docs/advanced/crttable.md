---
hide:
  - toc
---

Here's a table that shows you what options correlate to what video connection, to make it a bit easier to decide what you need in order to connect to your CRT, and what settings are required in the MiSTer.ini to get it to work. There is also a physical switch on the Analog IO board, in this table it is referred to as "SoG Switch". And finally there is a column for "Force Scandoubler" which is a setting in almost every MiSTer core in the OSD, usually under "Audio & Video".

## CRT Configuration Table

| Analog Video Out   | composite_sync= | ypbpr= | vga_sog= | direct_video= | vga_scaler= | forced_scandoubler= | SoG Switch |
| ------------------ | :-------------: | :----: | :------: | :-----------: | :---------: | :-----------------: | :--------: |
| RGBS Native        | 1               | 0      | 0        | 0             | 0           | 0                   | AUTO       |
| RGBS Scan-doubled¹ | 1               | 0      | 0        | 0             | 0           | 1                   | AUTO       |
| RGBS Upscaled²     | 1               | 0      | 0        | 0             | 1           | 0                   | AUTO       |
| RGBS Direct³       | 1               | 0      | 0        | 1             | 0           | 0                   | N/A        |
| RGBHV Native       | 0               | 0      | 0        | 0             | 0           | 0                   | AUTO       |
| RGBHV Scan-doubled | 0               | 0      | 0        | 0             | 0           | 1                   | AUTO       |
| RGBHV Upscaled²    | 0               | 0      | 0        | 0             | 1           | 0                   | AUTO       |
| RGBHV Direct³      | 0               | 0      | 0        | 1             | 0           | 0                   | N/A        |
| RGsB Native        | 1               | 0      | 1        | 0             | 0           | 0                   | AUTO       |
| RGsB Scan-doubled¹ | 1               | 0      | 1        | 0             | 0           | 1                   | AUTO       |
| RGsB Upscaled²     | 1               | 0      | 1        | 0             | 1           | 0                   | AUTO       |
| RGsB Direct³       | 1               | 0      | 1        | 1             | 0           | 0                   | N/A        |
| YPbPr Native       | 0               | 1      | 1        | 0             | 0           | 0                   | OVR        |
| YPbPr Scan-doubled | 0               | 1      | 1        | 0             | 0           | 1                   | OVR        |
| YPbPr Upscaled²    | 0               | 1      | 1        | 0             | 1           | 0                   | OVR        |
| YPbPr Direct³⁴     | 0               | 1      | 0        | 1             | 0           | 0                   | N/A        |
| S-Video⁵           | 1               | 0      | 0        | 0             | 0           | 0                   | N/A        |
| Composite⁵         | 1               | 0      | 0        | 0             | 0           | 0                   | N/A        |

¹ Scan-doubled = 2x resolution (e.g. 240p > 480p)  
² Upscaled resolution = video_mode  
³ External "direct video" (HDMI to VGA) adapter required - native resolution only (no upscaling or scan-doubling  
⁴ External "direct video" adapter requires modification to pass Sync on Green (SoG)  
⁵ External RGB to NTSC/PAL converter or Unofficial Y/C Core required

Credit: [Porkchop Express](https://twitter.com/MisterAddons){target=_blank}
