MiSTer has a built-in scaler which converts the low-resolution video directly from the cores to a higher resolution with the added capability of using filters and such to enhance the experience on modern displays. Here's an overview of how to configure the scaling ratios.

## Video Scale Mode (vscale_mode)
In your [MiSTer.ini file](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini){target=_blank} at the root of your MicroSD card you can modify the way the original video from the core is scaled up onto your display. If you read the section from the link just now you will see the following a few lines down:

```ini
vscale_mode=0          ; 0 - scale to fit the screen height.
                       ; 1 - use integer scale only.
                       ; 2 - use 0.5 steps of scale.
                       ; 3 - use 0.25 steps of scale.
                       ; 4 - integer resolution scaling, use core aspect ratio
                       ; 5 - integer resolution scaling, maintain display aspect ratio
```

There are a lot of options here so let's go through all of them:

### vscale_mode=0 (Fit Vertically to the Display Height)
This is the default setting when you first turn on your MiSTer. If the game resolution is 256x224, in order to fit it vertically into a 1920x1080p display, you have to divide 224 into 1080. However, 224 doesn't divide evenly into 1080 (`1080 / 224 = 4.821428571428571~`). So some of the pixels may not be scaled evenly. Some people don't mind this and it sure is nice to fill the screen entirely from top to bottom. You may see some shimmering pixels, if you do then use the interpolation video preset to alleviate this, or some of the adaptive scanline filters.

### vscale_mode=1 (Integer Scaling)
This setting makes it so the final scaled resolution multiplier of the core's video output is a whole number (e.g. 2x, 3x, 4x, 5x, 6x, etc...). Since your `#!ini video_mode` may still be set to 1920x1080p resolution, then the previous example of 256x224 will be scaled 4 times as large. `4 * 224 = 896`. However, the remainder is left black, so there will be a border, but your pixels are correctly scaled so there should be no shimmering (unless your display is causing it). Some people prefer this setting to get the crispest pixels they can get with a much lower chance of video artifacts that are undesirable. Others may not like it because it doesn't fill the screen the way 0 does.

### vscale_mode=2 and 3 (Fractional Integer Scaling)
This setting is similar to `#!ini vscale_mode=1`, however instead of scaling increments of whole numbers (e.g. 2x, 3x, 4x, etc...), it will scale in increments of fractions of either 0.5 (e.g. 2x, 2.5x, 3x, 3.5x, 4x, etc...) or 0.25 (e.g. 2x, 2.25x, 2.5x, 2.75x, 3x, etc...). For some monitors this setting can greatly reduces shimmering issues (although not all of it) while using sharper filtering (or no filtering at all). It's suggested to test around with vscale_mode 2 and 3 on a per core basis to see what looks best to your eyes.

### vscale_mode=4 and 5 (Dynamically Scaled Video Mode)
This setting was recently added by wickerwaka, and it dynamically changes your `#!ini video_mode` in order to retain an integer scaling but still fill the screen. It is ideal if you are using your MiSTer on a 2560x1440p or 4k display because you can scale vertically and still get very close to zero shimmering and video artifacts. The way this works may seem confusing but it's actually simpler than it seems. If you don't want to learn all about it, just change the setting and test it out yourself. If you want to know how it works, take a read below:

#### vscale_mode=4 (Integer Resolution Scaling which uses the Core's Aspect Ratio)
If you have `#!ini video_mode=13` set in your [MiSTer.ini file](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini){target=_blank}, then that means you are telling the MiSTer to set your display to 2048x1536p resolution at a 60hz refresh rate. 

If we take our example of 256x224, and let's assume the Core displays that at a 4:3 Aspect Ratio, then we need to find a vertical and horizontal resolution that fits the whole 256x224 at that ratio but Integer Scaled (like `#!ini vscale_mode=1` explained above). So 2048x1536 are actually the maximum numbers in either direction that we will go. 224 goes into 1536 almost 7 times but not quite, so the MiSTer will have to go with 6 as it's multiplier. That means the vertical resolution will be 1344. What is the horizontal resolution going to be? Well it has to be a 4:3 aspect ratio, so we also need to scale the 256 an equivalent amount. I personally use a [calculator like this](https://andrew.hedges.name/experiments/aspect_ratio/){target=_blank} when I want to find out what it should be. This tells me that my horizontal resolution should be 1792 in order to fit into that frame.

That looks like a **lot** of work, but thankfully vscale_mode=4 does all of the math for you so you don't have to worry about it so much. 

You may have mixed results with vscale_mode=4, for instance the PSX core changing resolutions will prompt a full resync, which can be jarring to some people.

#### vscale_mode=5 (Integer Resolution Scaling but maintaining the Display's Aspect Ratio)
This works very similarly to `#!ini vscale_mode=4` but it disregards the core's aspect ratio and it only calculates the proper integer scaled resolution that would fit in your screen's aspect ratio. Let's say you have a 1920x1200 display (16:10 aspect ratio) and you are using `#!ini video_mode=1920,1200,60`. The 16:10 aspect ratio will not be changed. This could be useful if you have a very specific display that you would like to fill up horizontally with some cores, or if you have a 31kHz computer monitor that does higher resolutions and you want to fit console cores into it's 4:3 aspect ratio.
