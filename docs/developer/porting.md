MiSTer uses quite complex hardware, but thanks to open source, developers with different levels of hardware/software knowledge can develop for this platform. Many cores for MiSTer use common almost identical part of code simplifying access to hardware and firmware called **Framework**.

We will use [ZX Spectrum](https://github.com/MiSTer-devel/ZX-Spectrum_MISTer){target=_blank} core as an example in this guide.

## Framework
Most of the sources of the Framework are located in [sys](https://github.com/MiSTer-devel/ZX-Spectrum_MISTer/tree/master/sys){target=_blank} folder.

Usually, for a new project, you need to take following files/folders:
* sys folder
* jtag.cdf
* jtag_lite.cdf
* zxspectrum.qpf (project file. Keep it read-only to prevent it from automatic changes whenever you switch between fill and lite versions and spam your change history)
* zxspectrum.qsf
* zxspectrum.srf (some warnings ignores)
* zxspectrum-lite.qsf
* zxspectrum-lite.srf (some warnings ignores)

You need to make some changes:
* Rename zxspectrum.* files according to a new project.
* Inside files find the "zxspectrum" word and replace it with the name of your project.
* in *.qsf files at the end you will find the list of project files. Remove files not related to your project.

The initial set of files for the new project is ready. Now you can open the project in Quartus 17.0 or higher.

Assuming you are porting some existing core to MiSTer, the top module entity should be renamed to emu. See zxspectrum.sv and its input/output signals:

```Verilog
module emu
(
	//Master input clock
	input         CLK_50M,

	//Async reset from top-level module.
	//Can be used as initial reset.
	input         RESET,

	//Must be passed to hps_io module
	inout  [48:0] HPS_BUS,

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

	output        LED_USER,  // 1 - ON, 0 - OFF.

	// b[1]: 0 - LED status is system status OR'd with b[0]
	//       1 - LED status is controled solely by b[0]
	// hint: supply 2'b00 to let the system control the LED.
	output  [1:0] LED_POWER,
	output  [1:0] LED_DISK,

	// I/O board button press simulation (active high)
	// b[1]: user button
	// b[0]: osd button
	output  [1:0] BUTTONS,

	input         CLK_AUDIO, // 24.576 MHz
	output [15:0] AUDIO_L,
	output [15:0] AUDIO_R,
	output        AUDIO_S,   // 1 - signed audio samples, 0 - unsigned
	output  [1:0] AUDIO_MIX, // 0 - no mix, 1 - 25%, 2 - 50%, 3 - 100% (mono)

	//ADC
	inout   [3:0] ADC_BUS,

	//SD-SPI
	output        SD_SCK,
	output        SD_MOSI,
	input         SD_MISO,
	output        SD_CS,
	input         SD_CD,

	//High latency DDR3 RAM interface
	//Use for non-critical time purposes
	output        DDRAM_CLK,
	input         DDRAM_BUSY,
	output  [7:0] DDRAM_BURSTCNT,
	output [28:0] DDRAM_ADDR,
	input  [63:0] DDRAM_DOUT,
	input         DDRAM_DOUT_READY,
	output        DDRAM_RD,
	output [63:0] DDRAM_DIN,
	output  [7:0] DDRAM_BE,
	output        DDRAM_WE,

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

    // there are more needed signals - see the Template_MiSTer repository
);
```
These signals are main connections to MiSTer. You need to modify your core according to these signals.

## API
Most top-level signals should be self-descriptive and more or less familiar to core developers, so I won't go too deep into it. I will describe some important parts where you need to pay attention to make your core work.

```verilog
input   RESET
```

This signal is asserted while ARM part is under initial preparation. It can be used as an initial reset. It won't be asserted anymore during the whole work of core except when the user chooses another core from OSD. Then ARM will assert RESET in the existing core to let it stop any possible activity before switching to another core (cores loaded through USB Blaster won't get "bye-bye" RESET).

If core uses DDR3 memory (Scaler isn't counted) then initial and bye-bye RESET is crucial for correct work. You will get a hard hang if DDR3 is accessed during RESET.

```verilog
inout  [48:0] HPS_BUS
```

Pass it as-is to hps_io module.

```verilog
output        CLK_VIDEO,
output        CE_PIXEL,
output  [12:0] VIDEO_ARX,
output  [12:0] VIDEO_ARY,
output        VGA_DE,
```

Besides other well-known VGA_* signals, these signals are important in MiSTer in order to get a proper display. CLK_VIDEO and CE_PIXEL are used to sample the pixels. If pixel rate equals to CLK_VIDEO, then set CE_PIXEL=1. Many cores have common system clock where pixel frequency is the product of the division of system clock to some number. In this case, set CLK)VIDEO to the system clock and assert CE_PIXEL at clock cycles where a new pixel is produced. Look in zxspectrum.sv to see how it's done.

Without CLK_VIDEO, you can still have VGA output, but OSD won't work.

**VIDEO_ARX** and **VIDEO_ARY** define aspect ratio on HDMI output. It doesn't affect VGA output. Usually VIDEO_ARX=4, VIDEO_ARY=3 or VIDEO_ARX=16, VIDEO_ARY=9. They can have other values but with extreme values, you may have video problems.

**VGA_DE** is another crucial part for MiSTer. Basically, it's opposite to blank signals: `~(VBlank | HBlank)` but with some notes. HDMI video scaler detects the horizontal resolution by first active video line. So, you need to be sure the first line is not cut due to unaligned VBlank and HBlank signals to each other. Otherwise, you will get a messed HDMI video.

**VGA_HS** and **VGA_VS** should have positive pulse polarity.

```verilog
output        AUDIO_S
```

Make sure you set correct mode signed/unsigned, otherwise audio will be distorted.

**DDRAM_** are signals of DDR3 memory. If the core can use this memory instead of SDRAM, then it won't require SDRAM board.

**SDRAM_** are signals of SDR SDRAM memory. The core will require SDRAM board if it uses these signals.

## HPS_IO
There is a supplementary module **hps_io.v** which is also required to use in the same entity (see zxspectrum.sv). It provides in/out control from ARM side. Most signals are same or similar to MiST (user_io+data_io or mist_io modules) signals. So, if the core is ported from MiST, it in most cases it's 1:1 signal connections.

MiSTer has some changes/improvements over original MiST io modules:
* Supports up to 4 images mount at the same time (MiST has only 1). Set module parameter VDNUM to 2..4 if more than 1 mounted image is required. If VDNUM=1 then related signals are same as in MiST.
* Due to SD card on MiSTer uses multiple partitions and holds other vital to MiSTer parts, access to whole SD card from cores is not available in MiSTer. Only the access to image files is possible. Cores requiring direct access to whole SD card should be redesigned to access to images only.
* Main MiSTer file system on SD card is exFAT which supports files bigger than 4GB.
* OSD supports up to 15 lines (7 lines in MiST) which is handy for many cores.
* ARM<->FPGA communication is done through the parallel bus which speeds up the communication. It supports 16bit I/O.

There are some other under the hood improvements in firmware like Keyboard/Mouse/Joystick setup.
