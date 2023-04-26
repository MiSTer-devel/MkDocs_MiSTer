In order to facilitate the dynamic saving and loading of savestates, MiSTer defines a special API specifically for fast restore and resume. Enabling the savestate functionality on your core reserves a developer-specified section of DDR3 memory, which is used for fast savestate reads/writes. It does **NOT** provide any functionality for the actual saving/loading of all registers and memories in your project.

**NOTE:** MiSTer is currently limited in the firmware to precisely four savestate slots. You cannot add more slots using this API.

## Setup

As specified in the [Core Configuration String](conf_str.md), a core name definition can be followed by `SS{base addr}:{savestate size}`, which declares the core as using savestates. In practice, it would look something like this: `MyCore;SS3E000000:1000;`. This declares the savestates will begin at `0x3E00_0000`, and each one will be allocated `0x1000` _bytes_. Note that the actual size on disk for the savestate does not have to match this allocated size; it just must be less than or equal to it. You probably want to choose this value to be a nice power of two, so that savestate slots 1-3 start at nice addresses.

**NOTE:** Most of the DDR controllers in various MiSTer projects hardcode the addresses to be in the `0x3000_0000` range, to give ample room to the MiSTer framework and CPU.

## Usage

The first 64 bit word of each savestate block (so `0x0`, `0x1000`, `0x2000`, etc. from our example) contains two 32 bit values. The lowest 32 bits (`[31:0]`) act as a change detector. The higher 32 bits (`[63:32]`) store the size of the savestate.

### Change Detector

The change detector notifies the MiSTer firmware that a savestate has been updated, and thus must be saved to disk. Saves are performed rather quickly after the write occurs, and do not require opening of the OSD, as block device saves do. While this value is persisted to disk as a part of the savestate writing process, it is not read again, and will be reset to `0xFFFF_FFFF` on restarting the core or loading a new ROM.

### Savestate Size

The savestate size word defines the number of 32 bit words that should be read for the savestate, not including the initial 64 bit control word. For example, to fetch 64 bytes, you would want to set this value to `64 / 4 = 16`. This value can vary between each of the 4 savestate slots if you so desire, as it is independant per slot.

On core launch, slots that are occupied will have the size word set, in addition to actually representing the current file contents. Empty slots will be initialized to 0.

### Actual Data

After the initial 64 bits of control data, the remaining address space up until the `savestate size` defined in `CONF_STR` is available to use as you will. You can read and write to this entire space as you'd like, and data will be persisted only on a change to the first word, according to the configured control size. This space is only initialized when there is a savestate file in that slot, and otherwise will contain random data. Remember that only the data denoted by the savestate size word will be persisted.

### Data on Disk

The file persisted to disk will be of size `savestate size control value + 2` in 32 bit words, that is, the size of the actual savestate contents, and an extra 64 bits for the control data at the start of the block.