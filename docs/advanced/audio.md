---
hide:
  - toc
---

The MiSTer has audio filters that you can use to make the audio sound less harsh and balanced to your ears. Some old game systems were not made for raw digital output, they had analog audio filters in place before the sound reached the speakers and your ears. These filters are generated using mathematical formulas to represent real common filters used in electronics. You can find all of the filters in the [Filters_MiSTer Github Repository](https://github.com/MiSTer-devel/Filters_MiSTer){target=_blank}.

## Types of Filters

`Arcade LPF` - The filters contained within this folder are designed to replicate the filtering of common arcade cabinets. Many arcade games' raw audio output is very harsh on the ears, and using the filters in here can help soften the sound to be more pleasing. 1st and 2nd refers to the amount of passes the filter goes through. LPF stands for "low-pass filter". The #khz tells you what frequency it starts filtering at.

`Core Specific` - These are for specific cores. Currently there is only one core-specific filter and it is in order to replicate the filtering of one model of Super Nintendo.

`General LPF` - These are more generalized low pass filters. The filters in this folder have a significantly different cutoff frequency when compared to the arcade cores.

## Audio Filtering Example Video
![type:video](videos/sound-filters.mp4)
