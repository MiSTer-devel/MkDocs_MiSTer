Many MiSTer cores have the capability to let you save your game, whether it be with traditional simulation of the original save features from the hardware, or with savestates. Most cores don't have savestates but a steadily increasing number do. Here's some basic information regarding how saves work on the MiSTer.

## Normal game saves

MiSTer will only update your normal game saves when you open the On-Screen Display (OSD). You will need to save inside the game, then open the OSD, and select "Save Backup RAM". In most cores, after you select this, you will need to open the OSD again and you should see a "Saving..." pop up on the screen. If you don't see this, then your game save likely didn't get updated. When a save is happening with the OSD open the yellow light on your Digital IO or Analog IO add-on board will be lit and will turn off when the save is completed.

Opening the OSD to save can be a bit of an adjustment at first, but it is necessary. It is intended behavior as MicroSD cards have a limited number of writes until they begin to fail. Also, since these cores are in FPGA, some cores may write to your MicroSD constantly multiple times a second if there wasn't a *signal* to tell the core to backup the save to a file.

## Autosave option

It's best to utilize the autosave option in any core. First open the OSD. Next, go to the Autosave option if it is available, and turn it on. Finally, go to the secondary OSD menu by pressing Right on your controller (or keyboard) and go to "Save Settings" to save the settings you changed in the OSD for that core. This will only save it for that one core, it won't save it for all the other cores, so keep that in mind. 

Almost every core does not autosave by default. Autosave being on would generate too many writes to the MicroSD card and could lead to earlier hardware failure, so this decision is deliberate.

## Save file conversion

The save file formats in most MiSTer cores are compatible with many popular emulators. However, some are different, so you may need to convert them. Thankfully Euan Forrester has made a save file converter that you can use to convert your saves into a MiSTer-compatible file.

[MiSTer Save File Converter](https://savefileconverter.com/#/mister){target=_blank}

Euan's tool also lets you convert many other save file formats from various emulators, and you can convert your MiSTer saves back into ones that are compatible with emulators.

## Backup your saves

Make sure to backup your saves off of the MicroSD regularly if you'd like to keep them safe. When MicroSD storage fails, it's usually swift and catastrophic. There are various tools to accomplish this with. One tool like this is [FreeFileSync](https://freefilesync.org/){target=_blank}. With FreeFileSync you can setup a scheduled batch job to backup specific folders from your MiSTer regularly. Read the documentation on FreeFileSync's website for more information.
