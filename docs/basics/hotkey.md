Here's a reference of the hotkeys you can use with the MiSTer. Hotkeys are useful at saving time and there are some hotkeys which do things you can only do with a keyboard or gamepad. Some of these hotkeys only work in the Main Menu core, others will work inside emulators as part of the gameplay, and some will work in all instances.

## In any core, with OSD closed

| Hotkey                                    | Description                                                                        |
| ----------------------------------------- | ---------------------------------------------------------------------------------- |
| ++f12++                                   | Open the Menu/On-Screen Display                                                    |
| ++alt+f12++                               | Open core select menu                                                              |
| ++win+prtsc++                             | Take a screenshot (upscaled)                                                       |
| ++shift+win+prtsc++                       | Take a screenshot (raw output)                                                     |
| ++lctrl+lalt+ralt++                       | Press "User" button, usually resets current core, same function as IO board button |
| ++lshift+lctrl+lalt+ralt++                | Full Reboot/Reset, same as IO add-on board Reset button                            |
| Controller: Button + Menu hotkey          | Turn on/off turbo/autofire for the pressed button                                  |
| Controller: Direction + Menu hotkey       | Set rate of turbo/autofire in milliseconds (ms)                                    |

## With the OSD open, in any core

| Hotkey                     | Description                                                             |
| -------------------------- | ----------------------------------------------------------------------- |
| ++f12++                    | Close OSD                                                               |
| ++f11++                    | Pair Bluetooth controller                                               |
| Hold IO Board OSD Button   | Alternate method to Pair Bluetooth controller
| Left                       | Go to information screen (shows currently selected INI file and volume) |
| Right                      | System screen (change core, set filters, gamma, etc...)                 |
| Controller: Back + R/L/D/U | Select Alternate INI file if defined (Default/Alt1/Alt2/Alt3)           |
| Controller: Select         | Expands submenus in the OSD when highlighted                            |

## In the Main Menu core only

| Hotkey                    | Description                                                              |
| ------------------------- | ------------------------------------------------------------------------ |
| ++f1++                    | Switch background type (static, wallpaper, color bars, black)            |
| ++f2++                    | Hide / Show core dates                                                   |
| ++f9++                    | Open Linux terminal / command line interface, use F12 to go back to menu |
| Controller: **x** / **y** | Test the rumble motors on your controller                                |

## Core-specific hotkeys

### Some computer cores

Some computer cores make use of the Windows key (++win++) on your keyboard.

| Hotkey      | Description  |
| ----------- | ------------ |
| ++win+f12++ | Open the OSD |

### Cores that support savestates

Very few cores support savestates (NES, PSX, GameBoy, GBA, WonderSwan, AtariLynx). There are 4 savestate slots available. In those cores there is a standard savestate button you can assign on your controller (we'll call that SaveStateBtn here):

| Hotkey                                  | Description                                   |
| --------------------------------------- | --------------------------------------------- |
| ++alt+f1++ - ++f4++                     | Save the state in slots 1-4 respectively      | 
| ++f1++ - ++f4++                         | Restore the state from slots 1-4 respectively |
| Controller: SaveStateBtn + Left/Right   | Switches the savestate slot                   |
| Controller: SaveStateBtn + Start + Down | Saves to the selected slot                    |
| Controller: SaveStateBtn + Start + Up   | Restores from the selected slot               |
