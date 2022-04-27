There are a few different ways you can use your MiSTer with a classic CRT display. The two main methods are either using the VGA port on the Analog IO board or using a specific Direct Video HDMI to VGA adapter.

## Configuration Table

Here's a table that shows you what options correlate to what video connection, to make it a bit easier to decide what you need in order to connect to your CRT, and what settings are required in the MiSTer.ini to get it to work.

|   Analog Video Out    | Ini: CSYNC | Ini: YPbPr | Ini: VGA_SOG | SoG Switch | VGA Scaler | Forced Scandoubler |
| --------------------- | ---------- | ---------- | ------------ |---------- | ---------- | ------------------ |
| RGBS Native           |      1     |      0     |      0       |   AUTO    |      0     |          0         |
| RGBS Scan-doubled¹    |      1     |      0     |      0       |   AUTO    |      0     |          1         |
| RGBS Upscaled²        |      1     |      0     |      0       |   AUTO    |      1     |          0         |
| RGBS Direct³          |      1     |      0     |      0       |    N/A    |      0     |          0         |
| RGBHV Native          |      0     |      0     |      0       |   AUTO    |      0     |          0         |
| RGBHV Scan-doubled    |      0     |      0     |      0       |   AUTO    |      0     |          1         |
| RGBHV Upscaled²       |      0     |      0     |      0       |   AUTO    |      1     |          0         |
| RGBHV Direct³         |      0     |      0     |      0       |    N/A    |      0     |          0         |
| RGsB Native           |      1     |      0     |      1       |   AUTO    |      0     |          0         |
| RGsB Scan-doubled¹    |      1     |      0     |      1       |   AUTO    |      0     |          1         |
| RGsB Upscaled²        |      1     |      0     |      1       |   AUTO    |      1     |          0         |
| RGsB Direct³          |      1     |      0     |      1       |    N/A    |      0     |          0         |
| YPbPr Native          |      0     |      1     |      1       |    OVR    |      0     |          0         |
| YPbPr Scan-doubled    |      0     |      1     |      1       |    OVR    |      0     |          1         |
| YPbPr Upscaled²       |      0     |      1     |      1       |    OVR    |      1     |          0         |
| YPbPr Direct³⁴        |      0     |      1     |      1       |    N/A    |      0     |          0         |
| S-Video⁵              |      1     |      0     |      0       |    N/A    |      0     |          0         |
| Composite⁵            |      1     |      0     |      0       |    N/A    |      0     |          0         |

¹ Scan-doubled = 2x resolution (e.g. 240p > 480p)  
² Upscaled resolution = video_mode  
³ External "direct video" (HDMI to VGA) adapter required - native resolution only (no upscaling or scan-doubling  
⁴ External "direct video" adapter requires modification to pass Sync on Green (SoG)  
⁵ External RGB to NTSC/PAL converter required

Credit: [Porkchop Express](https://twitter.com/MisterAddons){target=_blank}

For more detailed information than this table provides, read on below.

## MiSTer CRT Connectivity Options

*most of this content is from the guide written by [MikeS11](https://github.com/MikeS11/){target=_blank} and [ArchiveRL](https://github.com/ArchiveRL/){target=_blank} on the MiSTer FPGA GitHub Wiki*
### Boards / Converters

You can connect MiSTer natively to a CRT set using two methods: either by installing the analogue I/O board and using its VGA output or by connecting an HDMI-to-VGA DAC dongle directly to DE10 Nano's HDMI socket. Both of these methods produce nearly identical image which in most cases should match the output of the original hardware 1:1. Apart from that, they also have their specific pros & cons:

* Analogue I/O board 
  * Pros: extra features (buttons, led lights, etc), doesn't need SoG mod to connect to component
  * Cons: more expensive, lesser colour depth in some cores, can't use 2xSDRAM 
* Direct Video 
  * Pros: better colour depth, much cheaper
  * Cons: no extra features, needs extra modification for component, not all the dongles are guaranteed to work 

Once you have acquired either an I/O board or a Direct video adapter, you will need to connect it to your TV via a cable and also change some settings in the mister.ini file.

### Cables

* for consumer TVs (15kHz) with RGB SCART (via both I/O board & Direct Video) - Apart from I/O board or Direct Video dongle you'll also need a special cable. You can either make one or buy it online. [It's recommended](https://www.retrorgb.com/beware-of-mister-scart-cables.html){target=_blank} to get a cable with a 470 ohm resistor on the Composite Sync line (best ask the seller if it already has one)
  
  * Here are some possible sources: [Misteraddons (US)](https://misteraddons.com/collections/parts/products/video-cables-hdmi-scart-ypbpr){target=_blank}, [Retro Access (UK)](https://retro-access.com/products/mister-io-scart?_pos=1&_sid=97cb11000&_ss=r){target=_blank}, [Ultimatemister (PT)](https://ultimatemister.com/product/rgb-scart-cable/){target=_blank}, [Wolfsoft (DE)](https://www.wolfsoft.de/shop/product_info.php/products_id/15401//mister-premium-rgb-kabel-2m.html){target=_blank}, [Antoniovillena (ES)](https://www.antoniovillena.es/store/product/vga-scart-cable/){target=_blank}.
  
  * You can also get a MiST cable, it works in general but might be lacking the 470 Ohm resistor and is generally "not guaranteed": [Lotharek (PL)](https://lotharek.pl/productdetail.php?id=171){target=_blank}, [Amigastore (EU)](http://amigastore.eu/en/512-mist-scart-cable-mist-db15-f-to-scart-tv.html){target=_blank}.

  * Another option is to use a VGA-SCART converter, plus normal SCART/VGA cables. Possible sources: [Antoniovillena (SP)](https://www.antoniovillena.es/store/product/vga-scart-adapter/){target=_blank}, [Arcadeforge (DE)](https://arcadeforge.net/UMSA/UMSA-Ultimate-SCART-Adapter::57.html?language=en){target=_blank}, [Retro Upgrades (UK)](https://www.retroupgrades.co.uk/product/vga2scart/){target=_blank}.

  * If you are connecting to a consumer Trinitron you might also need to add an extra resistor/potentiometer to fix odd or not lively enough colours [forum link](https://misterfpga.org/viewtopic.php?p=4162#p4162){target=_blank}.

* consumer TVs (15kHz) with YPbPr component (via I/O board) - A standard VGA to Component cable should be enough.

* consumer TVs (15kHz) with YPbPr component (via Direct Video) - This will require cable modifications to add Sync on Green (SoG). Please read more here --> [Direct Video - Setup for YPbPr Signals](directvideo.md#setup-for-ypbpr-signals) or see what others have to say in the forum here -->  [Direct Video HDMI to Component CRT 480i TV by thorr](https://misterfpga.org/viewtopic.php?f=33&t=1471){target=_blank}.

* VGA monitors (31Khz) - A standard VGA cable should be enough.

* PVM/BVM monitors (via I/O board) - A standard VGA to BNC cable (3xRGB + HSync) cable should be ok.

* PVM/BVM monitors (via Direct Video) - A standard VGA to BNC cable (3xRGB + HSync) cable should be ok.

* Commodore monitors - A cable for the 1084S monitor is sold by [Ultimatemister (PT)](https://ultimatemister.com/product/mister-commodore-1084s/){target=_blank}.

### Settings

Most of the settings changes are done in your `MiSTer.ini` file, which is located in the `media/fat/` directory of your SD card. When editing this file, it is advised to backup your currently working `MiSTer.ini` file and then use a new `MiSTer.ini` from the official repository by [Right Clicking this link and clicking "save file as"](https://github.com/MiSTer-devel/Main_MiSTer/raw/master/MiSTer.ini){target=_blank}. All of the `MiSTer.ini` settings in this section assume you are using this default file. 

#### For I/O BOARD**

* consumer TVs (15kHz) with RGB SCART  
  `composite_sync=1`

* consumer TVs (15kHz) with Component  
  `ypbpr=1`  
  *You might need to flip the SoG switch on the I/O board*

* VGA monitors (31khz)  
  `forced_scandoubler=1`

#### For DIRECT VIDEO**

* consumer TVs (15kHz) with RGB SCART  
  `direct_video=1  `  
  `composite_sync=1`

* consumer TVs (15kHz) with Component  
  `direct_video=1  `  
  `composite_sync=1`  
  `ypbpr=1`

* VGA monitors (31khz)  
  `direct_video=1  `  
  `forced_scandoubler=1`

* for PVM/BVM monitors  
  `direct_video=1  `  
  `composite_sync=1`

### Connecting to Composite or S-Video

One method of obtaining Composite or S-Video on a capable CRT TV set is by using a special adapter. At the moment these are available for sale from [Antoniovillena](https://www.antoniovillena.es/store/product/vga-composite-s-video-adapter/){target=_blank} and [Ultimatemister (PT)](https://ultimatemister.com/product/mister-vga-to-composite-s-video/){target=_blank}.

There's also an open-source design which you can DIY: [Github](https://github.com/MikeS11/MiSTerCRT){target=_blank} / [forum link](https://misterfpga.org/viewtopic.php?f=33&t=2894){target=_blank}.

**These adapters have been reported to work well in S-Video mode, but Composite has problems with rainbow artifacting and excessive dot crawl. This is currently unavoidable and expected**

Another alternative is the [Axunworks converter](https://www.axunworks.com/RGB-to-Composite-S-Video-p341706.html){target=_blank}. It requires using a VGA-to-BNC cable with BNC-to-RCA adapters and most likely also suffers from artifacting in Composite [(forum thread)](https://shmups.system11.org/viewtopic.php?f=6&t=63452&start=270){target=_blank}.

### Unofficial Custom YC (S-Video / Composite) Cores by MikeS11
These requirements are for a [set of unofficial cores (currently in testing)](https://github.com/MikeS11/MiSTerFPGA_YC_Encoder/tree/main/YC%20Builds){target=_blank} that natively output s-video / composite directly from the core. The current cores generate two signals that use the existing RGB pins, where the luma (Brightness) uses the green output and the chroma (Color) uses the red output. Please do not report any bugs from using these cores in the official repositories, they are unofficial and in a testing state. It is possible that bugs could be induced by the changes made to the core.

#### Connection Requirements - S-Video

* A custom breakout board / cable the converts VGA to S-Video.
* VGA to Component Cable (Only required for some monitors, i.e Commodore 1702)
* Custom RCA to S-Video Connector

#### Connection Requirements - Composite

* A custom breakout board / cable the converts VGA to Composite
* VGA to Component Cable to a 1-Male to 2-Female RCA Y-Adapter Splitter Cable

*Note 1: It is recommended that you use a 0.47nF Capacitor in series with the Chroma signal. This will reduce the output voltage of your composite signal.*  
*Note 2: If using composite, it is recommended to use a breakout board with a luma trap that will filter out frequencies that confuse the tv from thinking brightness changes are color. (E.g Color Bleed & Rainbow Artifacting)*

### Using the Analog IO Board with the YC Test Cores

#### Configuration Requirements

- Sync on Green - ON
- Enable S-Video in the core menu

#### INI Settings
`vga_scaler=0`

### Using a Direct Video adapter with the YC Test Cores

#### Configuration Requirements
- A Sync On Green Circuit is Required. Please read more here: [Direct Video - Setup for YPbPr Signals](directvideo.md#setup-for-ypbpr-signals)
- Enable S-Video in the core menu

#### INI Settings
`YPbPr = 0`  
`Direct_video = 1`  
`Composite sync = 1`  
`vga_scaler=0`

More info & updates: [Twitter](https://twitter.com/MikeSimone3){target=_blank} / [S-Video Chroma Generation Document](https://docs.google.com/document/d/1FrfUKQedBdkgifHC88ouqLF9IDCNamC8TyLIcY3rou0/edit){target=_blank} [YC Core Clock Frequency List](https://docs.google.com/spreadsheets/d/12_6MyuY7f6CZYXztdT0C30SWL0nk2_MNe_Cno_D-txA/edit#gid=1960982362/){target=_blank} / [Forum Post: S-Video and Composite over Component output! (custom cores)](https://misterfpga.org/viewtopic.php?t=4434){target=_blank}

## Types of CRT Displays

There are three main categories of CRTs; Consumer Televisions, Computer Monitors, and Professional Video Monitors. Some of these overlap with compatibility, but often the signals intended for one type of CRT are not ideal on another type of display. There are also different subcategories of each of these that are not very important to go into here. Generally speaking, using a CRT with the MiSTer is not a one-size-fits-all experience.

### Consumer Televisions

Typically these are only compatible with a 15kHz frequency signal (the kind of signal video game consoles used). They were intended to be used with what is known as a "240p" analog signal. From the 1950's up until the late 1980's most consumer televisions only used [RF video](https://en.wikipedia.org/wiki/RF_connector){target=_blank} which is highly susceptible to interference, especially today. Later they began to use [composite video](https://en.wikipedia.org/wiki/Composite_video){target=_blank} (which is still very noisy, but less prone to interference than RF video). Some TV's would occasionally have support for [S-Video](){target=_blank} (a much sharper and nicer image quality and resistant to interference), but it is less common. In many European countries these TVs also supported RGB video by way of [SCART connectors](https://en.wikipedia.org/wiki/SCART){target=_blank} (which is about as good as it gets). Finally, near the end of the life of CRT televisions in the late 90's and early 2000's they began to use [Component video](){target=_blank} and even [HDMI video](https://en.wikipedia.org/wiki/HDMI){target=_blank}.

Most CRT televisions that you can buy used today (in the United States) are going to use composite video or component video. In europe it is more common, but still not a guarantee, to find CRT televisions with RGB SCART support used for sale.

### Computer Monitors

Usually computer monitors were designed for higher resolution 31kHz frequency signals. They often had support only for a [VGA connector](https://en.wikipedia.org/wiki/VGA_connector){target=_blank}, with some very few having some other options like [DVI connectors](https://en.wikipedia.org/wiki/Digital_Visual_Interface){target=_blank}. Since these displays were made for higher resolutions there can be some jitter or undesirable effects when attempting to run a lower resolution 240p signal through them, even if it is scandoubled to 31kHz. Computer Monitors are excellent at handling retro computer video signals as that is what they were designed for. There are also [Multisync Monitors](https://en.wikipedia.org/wiki/Multisync_monitor){target=_blank} which are capable of natively handling 15kHz (240p) analog signals. These are less common but are highly sought after by the CRT enthusiast community, so if you are interested in having one monitor to handle all types of signals, consider acquiring a Multisync monitor.

### Professional Video Monitors

Professional Video Monitors (PVMs) also go by many other names; [Broadcast reference monitor, Broadcast video monitor (BVM)](https://en.wikipedia.org/wiki/Broadcast_reference_monitor){target=_blank}, Medical Grade Monitor, and more. Simply put, these are displays designed for professional use that often are easy to do maintenance on, have high quality components, and were very costly for their time. Professional video monitors are still made today, but they are often OLED or LCD that are very expensive and only used in niche applications for businesses. These had a wide variety of connectivity that includes all of the previous mentioned connectors sometimes, and also had specialty connectors like [BNC connectors](https://en.wikipedia.org/wiki/BNC_connector){target=_blank} where the Red, Green, Blue, and sync signals were made into separate connectors. There are also BNC video cable configurations that require a fifth sync-on-green cable.

The benefit of purchasing a used professional video monitor CRT for use with retro hardware is that they have very high quality designs that have more lines displayed (crisper image), better colors, or superior display technology to that of consumer television CRTs overall. Additionally, they were often designed to be more easily serviceable and had better shielding against electromagnetic interference. Since around the mid 80's the majority of them seem to have supported native RGB input as well, so the video quality from your output source can be far superior, in theory. PVM's also typically allow for very granular control of the image through many control dials and buttons on the front. Many PVMs also support simultaneous output to mirror the image on one display to another. Finally, a good number of PVMs are also MultiSync, meaning they can support both 15kHz and 31kHz signals, and many of them also are region agnostic supporting 50hz PAL signals and 60hz NTSC signals.

Unfortunately, PVMs are incredibly expensive today, so if you don't already have one, it may be very difficult to get one now. It is not uncommon to see a mere 9" PVM selling for over $200 US Dollars with the 19" to  24" displays going anywhere from $500 to over $2000 US Dollars depending on the model's popularity and features.
