---
hide:
  - toc
---

There are a few different ways you can use a CRT display with the MiSTer. The two main methods are either using the VGA port on the Analog IO board or using a specific Direct Video HDMI to VGA adapter.

## Configuration Table

Here's a table that shows you what options correlate to what video connection, to make it a bit easier to decide what you need in order to connect to your CRT, and what settings are required in the MiSTer.ini to get it to work.

|   Analog Video Out    | Ini: CSYNC | Ini: YPbPr | SoG Switch | VGA Scaler | Forced Scandoubler |
| --------------------- | ---------- | ---------- | ---------- | ---------- | ------------------ |
| RGBS Native           |      1     |      0     |    AUTO    |      0     |          0         |
| RGBS Scan-doubled¹    |      1     |      0     |    AUTO    |      0     |          1         |
| RGBS Upscaled²        |      1     |      0     |    AUTO    |      1     |          0         |
| RGBS Direct³          |      1     |      0     |     N/A    |      0     |          0         |
| RGBHV Native          |      0     |      0     |    AUTO    |      0     |          0         |
| RGBHV Scan-doubled    |      0     |      0     |    AUTO    |      0     |          1         |
| RGBHV Upscaled²       |      0     |      0     |    AUTO    |      1     |          0         |
| RGBHV Direct³         |      0     |      0     |     N/A    |      0     |          0         |
| YPbPr Native          |      0     |      1     |     OVR    |      0     |          0         |
| YPbPr Scan-doubled    |      0     |      1     |     OVR    |      0     |          1         |
| YPbPr Upscaled²       |      0     |      1     |     OVR    |      1     |          0         |
| YPbPr Direct³⁴        |      0     |      1     |     N/A    |      0     |          0         |
| S-Video⁵              |      1     |      0     |     N/A    |      0     |          0         |
| Composite⁵            |      1     |      0     |     N/A    |      0     |          0         |

¹ Scan-doubled = 2x resolution (e.g. 240p > 480p)  
² Upscaled resolution = video_mode  
³ External "direct video" (HDMI to VGA) adapter required - native resolution only (no upscaling or scan-doubling  
⁴ External "direct video" adapter requires modification to pass Sync on Green (SoG)  
⁵ External RGB to NTSC/PAL converter required

Credit: Porkchop Express

## Analog IO Add-on board

## Direct Video Adapter
