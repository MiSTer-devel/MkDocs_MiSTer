---
hide:
  - toc
---

MiSTer supports keyboard re-mapping which is useful for reduced size or localized keyboards. Key remapping is system wide, so every core will have same key mapping. Keep in mind there is no macro key functionality, so single keys are remapped to another single key. Some multimedia keys generate several [key codes](https://www.scs.stanford.edu/10wi-cs140/pintos/specs/kbd/scancodes-5.html){target=_blank} - these keys cannot be remapped. Each keyboard model has its own key map stored in `/media/fat/config/kbd_[VID]_[PID].map` file. To reset all keys to their default state, simply delete the appropriate map file which has the matching VenderID and ProductID in the filename. Key remapping is available through the Menu core only.

## Joystick emulation
Keyboards can be switched to joystick emulation. You need to define keys used for joystick emulation the same way you did for joysticks. Auto fire is also supported the same way as they are for joysticks (Menu+button). The button defined for "KBD TOGGLE" provides a quick switch between keyboard and joystick use for defined keys.

## Mouse emulation
Keyboards can be switched to mouse emulation. You need to define mouse emulation buttons in the Menu core the same way as for joystick, in the Define Gamepad menu option.

## Emulation switch
To switch between emulation modes press `NumLock` or `ScrLock` until the desired mode is selected. 

The switching sequence is `Mouse >> Joy1 >> Joy2 >> None`

The LEDs on your keyboard will display the emulation modes:
* Mouse emulation: NumLock LED + ScrLock LED
* Joystick 1 emulation: NumLock LED.
* Joystick 2 emulation: ScrLock LED.

## Common functional keys/combos used in cores
* `F12` - open/close OSD menu/submenu
* `Alt-F12` - quick core selection (like in Menu core).
* `LCtrl+LAlt+RAlt` - presses the "USER" button which usually is reset in emulated system.
* `LShift+LCtrl+LAlt+RAlt` - MiSTer reset (load Menu core).

### Notes:
* Some systems provide writing support which requires additional attention to how you reset/shutdown the MiSTer. MiSTer tries not to keep any pending writes and writes physically to the disk as soon as possible. Still, safer way to reset the MiSTer from core which probably was writing to disk recently is using combo `LShift+LCtrl+LAlt+RAlt` - this will flush all caches to disk before restart. Cores without write can be restarted by hard reset button or powered down without special attention.
* `LCtrl+LAlt+RAlt` sequence can be replaced by some other well known combos through INI file.
