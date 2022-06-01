On MiSTer the top level is inside [sys/sys_top.v](https://github.com/MiSTer-devel/Template_MiSTer/blob/master/sys/sys_top.v){target=_blank}. When writing or porting a MiSTer core, instead of telling quartus to use your own top, quartus uses sys_top, and it will call a module called emu that you need to provide. This will document the parameters that your top level will need to implement. The MiSTer sys_top will handle a lot of useful things like audio and HDMI video.

## Instantiating your core

Tour core should be inside an emu block, see the [Template Top Level](https://github.com/MiSTer-devel/Template_MiSTer/blob/master/mycore.sv){target=_blank} for an example. Some of the contents of this article regarding the code used might be outdated, always reference the Template in the link above for the latest framework version.

## Master input clock
```verilog
	//Master input clock
	input         CLK_50M,
```

Most cores will use the PLL which is instantiated from the sys folder, but the pll needs to live in the rtl folder off of the top level (at the same level as sys). This choice was made so that you can update the sys folder without losing the PLL configuration.

NOTE: For full compatibility with the existing sys architecture, keep the pll named 'pll' and the instance 'pll' as shown below. You can use the megawizard to edit the pll to modify the required frequencies etc... (including adding more outputs). If you don't have a pll create a new one, or use the one from the template. The sys_top.sdc requires the name for the pll and the instance name be correct.

```
wire clk_sys;
pll pll
(
	.refclk(CLK_50M),
	.rst(0),
	.outclk_0(clk_sys)
);
```

## Reset
```verilog
	//Async reset from top-level module.
	//Can be used as initial reset.
	input         RESET,
```

Normally the RESET line is used in conjunction with the button on the I/O board, as well as a status flag. Most cores use status bit 0 (this is reserved for a Soft Reset), and a CONF_STR that includes an option like: `"R0,Reset;"`

```verilog
wire reset = RESET | status[0] | buttons[1];
```

## HPS Bus

The HPS Bus is used to communicate with the ARM processor. It is passed into the hps_io module which will do a bunch of work for the core, and provide a simpler interface to use. Include the hps_io module in the emu module. See [hps_io](hps_io.md)

```verilog
	//Must be passed to hps_io module
	inout  [45:0] HPS_BUS,
```

## Video Signals

The top level module that calls emu includes the high quality HDMI scaler, and provides a fairly simple interface to output video on MiSTer. There are a number of other helper modules that can be included to provide proper video output.

At the simplest level provide a CLK_VIDEO, and/or CE_PIXEL (CE_PIXEL can be set to 1 if your video clk is correct). The video clock needs to be greater than 40MHZ for all of the features to work. 

Generally the video signals want to be whatever the native resolution of the machine that is being emulated. ie: an old 8bit computer will generally output 15khz video. MiSTer has a scandoubler built in that will create VGA compatible output if the user wants that on their VGA port. To include this scandoubler in the core you will usually use the video_mixer or arcade_video modules. The forced_scandoubler signal comes from the hps_io module. Some users want to use a 15khz monitor with 15khz cores, so the core itself shouldn't have a scandoubler built in. Some original devices may have had higher resolution output, if that native output was greater than 15khz, it is ok to output it natively through the VGA signals.  The scaler will use the VGA_DE (usually based on HBLANK and VBLANK `assign VGA_DE = ~(HBlank | VBlank);`)  to scale it up to HDMI based on the settings in the ini file.

### Video Mixer

Use the [Video Mixer](video_mixer.md) Module to add MiSTer framework standard features like gamma support, scaling, and scandoubling.

### Video Freak 

Use the [Video Freak](video_freak.md) Module to add cropping and scaling

### Arcade Video

Use the [Arcade Video](arcade_video.md) Module for arcade cores to support rotation, scandoubling, and most of the features that are in video_mixer. This file also includes **screen_rotate** which is used for vertical arcade games to allow rotation over HDMI.

```verilog
	//Base video clock. Usually equals to CLK_SYS.
	output        CLK_VIDEO,

	//Multiple resolutions are supported using different CE_PIXEL rates.
	//Must be based on CLK_VIDEO
	output        CE_PIXEL,

	//Video aspect ratio for HDMI. Most retro systems have ratio 4:3.
	//if VIDEO_ARX[12] or VIDEO_ARY[12] is set then [11:0] contains scaled size instead of aspect ratio.
	output [12:0] VIDEO_ARX,
	output [12:0] VIDEO_ARY,

	output  [7:0] VGA_R,
	output  [7:0] VGA_G,
	output  [7:0] VGA_B,
	output        VGA_HS,
	output        VGA_VS,
	output        VGA_DE,    // = ~(VBlank | HBlank)
	output        VGA_F1,
	output [1:0]  VGA_SL,
	output        VGA_SCALER, // Force VGA scaler

	input  [11:0] HDMI_WIDTH,
	input  [11:0] HDMI_HEIGHT,
	output        HDMI_FREEZE,

`ifdef MISTER_FB
	// Use framebuffer in DDRAM (USE_FB=1 in qsf)
	// FB_FORMAT:
	//    [2:0] : 011=8bpp(palette) 100=16bpp 101=24bpp 110=32bpp
	//    [3]   : 0=16bits 565 1=16bits 1555
	//    [4]   : 0=RGB  1=BGR (for 16/24/32 modes)
	//
	// FB_STRIDE either 0 (rounded to 256 bytes) or multiple of pixel size (in bytes)
	output        FB_EN,
	output  [4:0] FB_FORMAT,
	output [11:0] FB_WIDTH,
	output [11:0] FB_HEIGHT,
	output [31:0] FB_BASE,
	output [13:0] FB_STRIDE,
	input         FB_VBL,
	input         FB_LL,
	output        FB_FORCE_BLANK,

`ifdef MISTER_FB_PALETTE
	// Palette control for 8bit modes.
	// Ignored for other video modes.
	output        FB_PAL_CLK,
	output  [7:0] FB_PAL_ADDR,
	output [23:0] FB_PAL_DOUT,
	input  [23:0] FB_PAL_DIN,
	output        FB_PAL_WR,
`endif
`endif
```

## LEDs on the IO board

```verilog
	output        LED_USER,  // 1 - ON, 0 - OFF.

	// b[1]: 0 - LED status is system status OR'd with b[0]
	//       1 - LED status is controled solely by b[0]
	// hint: supply 2'b00 to let the system control the LED.
	output  [1:0] LED_POWER,
	output  [1:0] LED_DISK,
```

## Buttons on IO board

```verilog
	// I/O board button press simulation (active high)
	// b[1]: user button
	// b[0]: osd button
	output  [1:0] BUTTONS,
```

## Audio
```verilog
	input         CLK_AUDIO, // 24.576 MHz
	output [15:0] AUDIO_L,
	output [15:0] AUDIO_R,
	output        AUDIO_S,   // 1 - signed audio samples, 0 - unsigned
	output  [1:0] AUDIO_MIX, // 0 - no mix, 1 - 25%, 2 - 50%, 3 - 100% (mono)
```

## A to D converter

Used for tape input and other things. An extra module on MiSTer that provides an analog audio jack, and conversion to digial signals.

```verilog
	//ADC
	inout   [3:0] ADC_BUS,
```

## Signals for the second SD card

```verilog
	//SD-SPI
	output        SD_SCK,
	output        SD_MOSI,
	input         SD_MISO,
	output        SD_CS,
	input         SD_CD,
```

## DDR3 Memory Subsystem

```verilog
	//High latency DDR3 RAM interface
	//Use for non-critical time purposes
	output        DDRAM_CLK,          // any clock, no restrictions. Typically main core clock
	input         DDRAM_BUSY,         // every read and write request is only accepted in a cycle where busy is low
	output  [7:0] DDRAM_BURSTCNT,     // amount of words to be written/read. Maximum is 128
	output [28:0] DDRAM_ADDR,         // starting address for read/write. In case of burst, the addresses will internally count up
	input  [63:0] DDRAM_DOUT,         // data coming from (burst) read
	input         DDRAM_DOUT_READY,   // high for 1 clock cycle for every 64 bit dataword requested via (burst) read request
	output        DDRAM_RD,           // request read at DDRAM_ADDR and DDRAM_BURSTCNT length
	output [63:0] DDRAM_DIN,          // data word to be written
	output  [7:0] DDRAM_BE,           // byte enable for each of the 8 bytes in DDRAM_DIN, only used for writing. (1=write, 0=ignore)
	output        DDRAM_WE,           // request write at DDRAM_ADDR with DDRAM_DIN data and DDRAM_BE mask
```

### Writing to DDR3

The internal DDR3 controller handles writes very efficiently, so burst writes are typically not required.
To write, DDRAM_WE should be high for 1 clock cycle whenever DDRAM_BUSY is low. 
It will write the data in DDRAM_DIN to DDRAM_ADDR with respect to DDRAM_BE.
For a single write, DDRAM_BURSTCNT should be 1.
Multiple writes can also be issued without pausing when DDRAM_BURSTCNT = 1.

### Reading from DDR3

To read one or multiple 64 bit words, DDRAM_RD must be high for 1 clock cycle, while DDRAM_BUSY is low.
It will read DDRAM_BURSTCNT 64 bit words from DDRAM_ADDR(counting up for bursts) and provide the results, typically one each clock cycle, at DDRAM_DOUT with DDRAM_DOUT_READY = 1, when the read is valid.
Every read request will have a latency of multiple cycles. Something like 20 cycles @ 100Mhz is a typical value, but it can be way longer.
DDR3 read should therefore be used with higher DDRAM_BURSTCNT to make use of the high bandwidth, whenever possible.

### DDR3 Busy signal

DDRAM_BUSY acts like an ignore for the request ports. So whenever this signal is high, no request can be issued in this clock cycle.
However, having a request pending doesn't lead to any problem, so it is uncritical to e.g. set DDRAM_RD = 1 in a clocked process and only clear it back to 0 when DDRAM_BUSY = 0.
This way, the request signals can be clocked instead of being combinatorial, leading to higher possible clock speed and less problems with timing closure.

## Single and Dual SDRAM interface

For full understanding of the SDRAM interface you will need to look at the specifications for the SDRAM chip. Also, the [hardware](https://github.com/MiSTer-devel/Hardware_MiSTer){target=_blank} may be useful, here is the [Schematic](https://github.com/MiSTer-devel/Hardware_MiSTer/blob/master/releases/sdram_xsds_2.9.pdf){target=_blank}. It is useful to look through some code that already runs on MiSTer:

Look through the data sheet for the [32MB](https://github.com/MiSTer-devel/Main_MiSTer/wiki/files/AS4C16M16SA-V3.0_March%202015.pdf){target=_blank} module. The 64MB module data sheet isn't as detailed.

Some examples of SDRAM modules:
* single port direct usage: [Gameboy](https://github.com/MiSTer-devel/Gameboy_MiSTer/blob/master/rtl/sdram.sv){target=_blank}
* multi port request/response: [Gameboy Advance](https://github.com/MiSTer-devel/GBA_MiSTer/blob/master/rtl/sdram.sv){target=_blank}
* complex bank machine: [JT Frame](https://github.com/jotego/jtframe/blob/master/hdl/sdram/jtframe_sdram_bank.v){target=_blank}

```verilog
	//SDRAM interface with lower latency
	output        SDRAM_CLK,
	output        SDRAM_CKE,
	output [12:0] SDRAM_A,
	output  [1:0] SDRAM_BA,
	inout  [15:0] SDRAM_DQ,
	output        SDRAM_DQML,
	output        SDRAM_DQMH,
	output        SDRAM_nCS,
	output        SDRAM_nCAS,
	output        SDRAM_nRAS,
	output        SDRAM_nWE,

`ifdef MISTER_DUAL_SDRAM
	//Secondary SDRAM
	//Set all output SDRAM_* signals to Z ASAP if SDRAM2_EN is 0
	input         SDRAM2_EN,
	output        SDRAM2_CLK,
	output [12:0] SDRAM2_A,
	output  [1:0] SDRAM2_BA,
	inout  [15:0] SDRAM2_DQ,
	output        SDRAM2_nCS,
	output        SDRAM2_nCAS,
	output        SDRAM2_nRAS,
	output        SDRAM2_nWE,
`endif
```

## Serial Support

Serial is passed to the linux arm side of the MiSTer. On the arm side, software decides what to do with the data. ie: send it to shell, ppp, MIDI, etc.

Different serial speeds and optons are set using options in the [CONF_STR](conf_str.md). 

```verilog
	input         UART_CTS,
	output        UART_RTS,
	input         UART_RXD,
	output        UART_TXD,
	output        UART_DTR,
	input         UART_DSR,
```

## User Port - extra USB 3.1A style connector on MiSTer


| USB  |  P7 |  Name  | PIN  |   MiSTer | emu wire |
|---|---|---|---|---|---|
|1  |  +5V |   +5V|
|2  |  2  |  TX   | SDA  |  AH9   | USER_IO[1] |
|3  |  1    |RX   | SCL   | AG11   | USER_IO[0] |
|4  |  GND   | GND|
|5  |  8   | DSR  |  IO10  |  AF15  |  USER_IO[5]|
|6  |  7   | DTR  |  IO11  | AG16   | USER_IO[4]|
|7  |  6   | CTS  |  IO12  |  AH11  |  USER_IO[3]|
|8  |  5   | RTS  |  IO13  |  AH12  |  USER_IO[2]|
|9  |  10  |  IO6 |   IO8  |  AF17  |  USER_IO[6]|
|10 |   Shield |   Shield |

```verilog
	// Open-drain User port.
	// 0 - D+/RX
	// 1 - D-/TX
	// 2..6 - USR2..USR6
	// Set USER_OUT to 1 to read from USER_IN.
	input   [6:0] USER_IN,
	output  [6:0] USER_OUT,
```

## OSD Status

This is set to 1 when the OSD is open. It can be used to pause the core when the OSD is open, and/or for autosave.

```verilog
	input         OSD_STATUS
```
