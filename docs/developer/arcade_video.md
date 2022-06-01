Arcade video is used mostly in arcade cores. It has some useful helpers to optionaly turn on scandoubler (based on the ini settings), deals with rotation on HDMI, and can optionally handle GAMMA, and different color widths.

## Instantiating arcade_video

The module has a few parameters that are used to set it up.

* WIDTH - the width of one scanline
* DW - width of pixels. most arcades don't use a full 24 bits
   *  6 : 2R 2G 2B
   *  8 : 3R 3G 2B
   *  9 : 3R 3G 3B
   * 12 : 4R 4G 4B
   * 24 : 8R 8G 8B
* GAMMA - allow gamma controls

The clk_video needs to be 4x the ce_pix and above 40MHZ.

```verilog

	input         clk_video,
	input         ce_pix,
```

The FX parameter uses the output of `status[5:3]` in this example of a config string: `"O35,Scandoubler Fx,None,HQ2x,CRT 25%,CRT 50%,CRT 75%;",`

## Rotating vertical games 

Optionally, we add the screen_rotate and pass in whether the game needs to rotate ccw or cw.

Screen rotate uses DDRAM for the framebuffer for rotation. If your core needs DDRAM for something else, see [MCR3](https://github.com/MiSTer-devel/Arcade-MCR3_MiSTer){target=_blank} for an example that uses DDRAM for an audio file and for the screen_rotate. Use this ddram: 

* [ddram](https://github.com/MiSTer-devel/Arcade-MCR3_MiSTer/blob/master/rtl/ddram.sv){target=_blank} instead of screen_rotate.

```verilog
screen_rotate screen_rotate
(
		  .*,
		  .rotate_ccw(ccw)
);

module arcade_video #(parameter WIDTH=320, DW=8, GAMMA=1)
(
	input         clk_video,
	input         ce_pix,

	input[DW-1:0] RGB_in,
	input         HBlank,
	input         VBlank,
	input         HSync,
	input         VSync,

	output        CLK_VIDEO,
	output        CE_PIXEL,
	output  [7:0] VGA_R,
	output  [7:0] VGA_G,
	output  [7:0] VGA_B,
	output        VGA_HS,
	output        VGA_VS,
	output        VGA_DE,
	output  [1:0] VGA_SL,

	input   [2:0] fx,
	input         forced_scandoubler,
	inout  [21:0] gamma_bus
);
```
