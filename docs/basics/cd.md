MiSTer supports Cue/Bin and [CHD](https://github.com/rtissera/libchdr){target=_blank} formats. The way the MiSTer handles CD-based ROMs and images is fairly simple. There are some specifics that need to be described about how the MiSTer handles CDs.

## Will MiSTer ever support USB CD Drives?

The short answer is **no**. The long answer is that 1) there is too much hardware variation in CD drives and the drivers that go with them for it to be worth it and 2) everything added to the Linux image and Main binary for the MiSTer have to be very carefully considered as the goal is to keep it lightweight and not bloated. 

CD Drive support is not a priority, as properly dumped CD-ROM images are bit-perfect where it counts (excluding randomized subchannel data and garbage data fill-in).

## Cue/Bin Folders and CHD files

If you are using cue/bin files, then you need to place them in their own folder separate from the other cue/bin ROMs. Currently every CD-based core supports cue/bin. CHD files are a compressed CD image format that is also supported by almost every CD-based core. CHD files don't need to be placed in their own folder separate from each other.
