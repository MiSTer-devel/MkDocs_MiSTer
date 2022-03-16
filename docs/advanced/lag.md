A common concern among retro enthusiasts is whether a device of this sort has _lag_ and whether it will create a less desirable experience compared to original hardware. 

Every electronic equipment exhibits some kind of _latency_, but it only becomes problematic if this latency causes frames to be missed. A frame is typically 16ms for a system using a 60 frames per second (60 Hz) display.

Lag is only problematic in a few specific cases:
* Some older games were designed to rely on extremely quick response times (e.g. Punch-Out on NES).
* If the latency is different between two players, it could introduce an unfair advantage.
* Lag that isn't constant can be an issue on games that require precise movement. (Most players can adapt to lag that is consistent.)

There are three major categories of lag. **Input**, which involves controllers, mouse, etc, **Processing**, which would involve buffering in the core, execution or delays in code and **Display** which involves the output of the video to your display device.

For a more detailed overview of lag and exploration of it, please refer to this page:

[https://inputlag.science/](https://inputlag.science/){target=_blank}

### Input
For input, MiSTer primarily uses USB. In this case the overall input lag is the sum of the lag caused by the USB polling and the lag caused by the controller itself, how quickly it processes the signals. The latter is outside the scope of MiSTer and can only be improved by using a better controller. On the MiSTer side only the lag caused by the USB polling can be reduced if the connected USB device supports a lower polling interval. The polling interval is measured in Hz and indicates how often a USB device is polled per second. At 1000 Hz, a USB device is polled 1000 times per second, which means the additional lag caused by the polling is 1 s / 1000 = 1 ms in the worst case and 0.5 ms on average. This is a great improvement compared to the default value of 125 Hz, where a USB device is polled 125 times per second, which means the additional lag caused by the polling is 1 s / 125 = 8 ms in the worst case and 4 ms on average.

If a game is rendered at 60 frames per second, a single frame takes 1 s / 60 ≈ 16 ms to process. One might think that any polling interval below 16 ms would be perfect; however, USB polling happens independently of the vertical sync. Therefore, even with a 1 ms polling interval, there is a chance of 1/16 that the whole frame will be missed and input will be processed on the next frame. The longer the polling interval, the greater the odds of a missed frame. With a polling interval of 8 ms, the odds of input missing a frame are 50%. Native polling rates and input response vary across consoles and even games.

### Processing
This is one core advantage of emulation using FPGAs. Unlike software emulators which go through a cycle of executing, and then waiting for a screen refresh, FPGA cores run in real time, as the original hardware did. This means that cores don’t have CPU bottlenecks to slow them down arbitrarily or require additional large buffers to hold data under most circumstances.

### Display
MiSTer’s two primary display outputs are analog and HDMI. 

The analog output is driven as the original system would have, with no buffering, and so it will be effectively identical to the latency of a real console. From this point of view, the analog output cannot have any form of lag. 

When using HDMI output the image must be scaled up to fit the higher resolutions, which requires additional processing. The MiSTer scaler has options which impact its latency. Using `vsync_adjust=2` in the ini file will result in about 4 scanlines of latency, while 0 or 1 will result in up to roughly 2 frames of latency, with the added advantage of being more compatible with displays. 

In addition your own television or monitor may introduce more latency, but this varies by device and no definite number can be given on that here. 

In summary, if lag is critical to you, **it's best to play on a CRT using a recommended and widely-tested USB controller.** Some users have tested and ranked USB controllers by performance; you can see their results [here](https://github.com/eniva/MisSTer_Guides/wiki/USB-Controllers-Performance-Ranking){target=_blank}. An alternate thorough list of tested controllers by misteraddons is also available [here](https://rpubs.com/misteraddons/inputlatency){target=_blank}.

Do keep in mind, however, that even over HDMI MiSTer is capable of providing a better experience than many other devices.

## Reducing Lag

### Video lag

MiSTer offers options in how to configure its HDMI upscaler, making a tradeoff between compatibility and low latency.
These can be set in the MiSTER.INI file at the root of the SD card:

* `vsync_adjust=2` is the best option if it is compatible with your TV. This mode uses the original refresh rate and pixel clock of the core, resulting in no additional latency.
* `vsync_adjust=1` is the second best option, but it adds up to 2 frames of latency. This mode uses a framebuffer but maintains the system's original vsync and varies the pixel clock per core.
* `vsync_adjust=0` is the lesser option, but the most compatible. Up to 2 frames of latency and less smooth scrolling. This mode guarantees 60 hz output with an NTSC standard pixel clock.

### Input lag

USB controllers usually have an interval value which the host (MiSTer Linux kernel) respects to poll their inputs at. Most USB devices can actually perform better by being polled more often without any side effects.

To set a higher USB polling rate, you need to go to the "linux" subdirectory on your SD card and rename "u-boot.txt_example" to "u-boot.txt". The aforementioned file contains the following options, which should only be changed if you are encountering problems:
```bash
v=loglevel=4 usbhid.jspoll=1 xpad.cpoll=1
```
**loglevel**: 4 is the default value. You can set this to 9 to get debugging messages with dmesg command via SSH. If you just want to know which values of usbhid.jspoll and xpad.cpoll are applied to your controller, there are easier ways to achieve this (see below).

**usbhid.jspoll**: specifies the interval for USB HID controllers, usually DirectInput.

* 0 is the default value MiSTer uses (even when there is no "u_boot.txt"). In this case the requested value from the controller is used.
* 1 is the recommended value (which means 1000/1 = 1000 Hz polling rate). However, if you ever encounter any issues, try higher integer values. The higher the interval, the higher the possible lag. This shouldn't go above 8 (which means 1000/8 = 125 Hz polling rate).
* To see which value is applied to your controller, you can run ```systool -m usbhid -A jspoll``` from the Linux shell.

**xpad.cpoll**: specifies the interval for USB XInput controllers. Most popular controllers use this. There is no practical difference here. XInput is for Microsoft's Xbox consoles and PC.

* 0 is the default value MiSTer uses (even when there is no "u_boot.txt"). In this case the requested value from the controller is used.
* 1 is the recommended value (which means 1000/1 = 1000 Hz polling rate). However, if you ever encounter any issues, try higher integer values. The higher the interval, the higher the possible lag. This shouldn't go above 8 (which means 1000/8 = 125 Hz polling rate).
* To see which value is applied to your controller, you can run ```systool -m xpad -A cpoll``` from the Linux shell.

## What is the fastest controller I can get?

Almost any standard USB controller will work well with MiSTer, however there is a short list of excellent controllers that we can suggest based on user feedback and input lag testing:

* 8bitdo M30 2.4g connected in wired mode
* Sony DS4 in wired mode
* Hori Fighting Commander (later revisions), either PS4 or XBOX1 variant is fine; pick your favorite
* DIY USB adapter using open source firmware available [here](https://github.com/MiSTer-devel/Retro-Controllers-USB-MiSTer){target=_blank}

Generally speaking, while Bluetooth connected devices will work fine, you can expect the highest amount of input latency while using your controller in this way.

Please keep in mind, “high latency” controllers *should* add, at most, 16 ms (1/60th of a second) or one frame (or rarely, depending on the controller, 32ms) of lag, and not constantly, to your experience, which is not a lot of lag, so if you’re not the type of person who notices that, you can safely just use any decent USB controller. Variable lag (the input response varying between 1 and 3 frames, for instance) is more noticeable than consistent lag. There are very few controllers which add more than 1 frame of lag.

There is no definitive fastest controller that you can get, but there are quite a few at the top of the list. You can, again, check MiSTerAddons and Lemonici's [MiSTer Input Latency Chart](https://rpubs.com/misteraddons/inputlatency){target=_blank} for a definitive community sourced list of controllers tested with MiSTer with a separate device that uses the DE10-Nano's headers to get an objective result.

Please see these article for more information about USB controller lag
* https://medium.com/@WydD/controller-input-lag-how-to-measure-it-1ebfd2c9d60
* https://inputlag.science/
