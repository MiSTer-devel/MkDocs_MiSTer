The standard paths are of the form `/media/fat/games/<CORE>`, where `<CORE>` is the [internal core name](../developer/corenames.md) of the given system. 

Please check the respective README file for each core to determine the appropriate full path.

## Standard USB Core Paths
They are of the form `/media/usb<0..5>/games/<CORE>`. Where `<0..5>` indicates the number of USB drives mounted by the operating system.

## Standard CIFS Core Paths
They are of the form `/media/fat/cifs/games/<CORE>`.

## Other Paths
There are other valid paths, that are available for backwards-compatibility reasons, and also to ease testing. You should use the standard paths instead whenever possible.

## Path Priority
There is a priority order of core paths. When you plug in a USB drive and it has a folder `/games/PSX` on it (mounted locally as `/media/usb<0..5>/games/PSX` when plugged in), then the MiSTer PSX core will look to that folder on the USB drive instead of the local one on the MicroSD at `/media/fat/games/PSX`. Here is the priority list from [Main_MiSTer's file_io.cpp](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/file_io.cpp#L922){target=_blank} in order of highest priority to lowest:

1. `/media/usb<0..5>`
2. `/media/usb<0..5>/games`
3. `/media/network`
4. `/media/network/games`
5. `/media/fat/cifs`
6. `/media/fat/cifs/games`
7. `/media/fat`
8. `/media/fat/games`

If the core's folder isn't found in any of these it should create the folder.
