---
hide:
  - toc
---

MiSTer has support for a wide variety of input devices. It also has options to configure these devices to fit your needs. Here is a breakdown of some special configurations for various input devices like spinners, gamepads, joysticks, and keyboards.

## What is supported?

Generally speaking, any normal USB HID compatible input device should work. Keyboards, arcade spinners, usb adapters for original controllers such as the Raphnet and Daemonbite retro adapters, and even modern console controllers like the DualSense PS5 controller. There is even the Serial Native Accessory Connector, if you have one of the Analog or Digital IO add-on boards, which on supported cores allows you to use original hardware controllers, such as lightguns, which would normally only work with the original system and require zero lag to function.

## Serial Native Accessory Convertor (SNAC)

SNAC adaptors allow you to connect original hardware controllers and peripherals to the MiSTer cores. The cores which support SNAC connections have been specially built to have serial connections exposed to specific pins on the DE10-Nano. That means when you pull the trigger on the NES Zapper while aiming at your CRT, the signals travel almost instantly, similar to how they would on original hardware.

## Using A Mouse

You can also use a mouse for various purposes on the MiSTer. The main purpose for mouse support is for use with some computer cores which had mice.

One of the cool things you can do is use the mouse as an emulated lightgun. The same principles behind doing this applies to a wiimote with a powered sensor bar. You can do this by pairing your wiimote to the MiSTer and it will be used as a Mouse when paired.

![type:video](videos/mouse-lightgun.mp4)

You can also use a mouse for a paddle style controller if you'd like.

## Are gaming keyboards worth it?

High performance and expensive keyboards and mice aren't advantageous to use for MiSTer. They won't give any major or even minor significant benefits. Additionally, these devices often have too many functions and many virtual devices cluttering the input subsystem which may introduce input lag or be complete unresponsive. They may also prevent other devices, such as gamepads, from working. So if you experience problems with your gaming keyboard, try a simpler keyboard instead to see if that resolves the issue. General advice is not to go out and buy a specialty gaming keyboard for MiSTer specifically, it may end up being a waste of money.

## What about rumble support?
Currently rumble support is not added into the framework. It will maybe come at a later time, but some cores do have the support built into them (GBA, etc...)so they are ready for when it is added.

## What about PS3/PS4/PS5, XBoxOne/360, Switch, and 8bitdo receivers/gamepads?
The ideal solution today for these types gamepads is to use 3rd-party receivers, such as 8bitdo retro receivers, specifically the 8Bitdo Wireless Bluetooth Adapter, or any number of name-brand Bluetooth 4.x/5.0 receivers. The 8bitdo receiver easily supports Xbox One S/X, PS3, PS4, Wii, Switch, and 8Bitdo's own gamepads and it can pair easily without using the bluetooth setup menu. One 8bitdo bluetooth receiver will pair with one controller at one time. If multiple controllers are required for multiplayer games, then multiple receivers will need to be purchased if you are using the 8bitdo receiver, however a regular Bluetooth usb receiver does not suffer from this limitation.

The 8bitdo receivers have been reported as having some lag introduced, limited range, and bad line of sight, when compared to Bluetooth 5.0 adapters (like the TP-Link and Asus ones). The main appeal of the 8bitdo receivers is the ease of use and quick pairing. The 8bitdo receivers act as a controller themselves and are a compatibility layer between your paired controller and whatever they are attached to via USB, for easy compatibility. Bluetooth adapters by comparison pair your controller itself directly as a device to the MiSTer. No matter what controller you connect, the 8bitdo receiver will see it as the same controller, the 8bitdo receiver's controller. This means that some features like the DualSense (PS5) controller's added mute button and touchpad will not be available, whereas using bluetooth 5.0 may run a very minor risk of limited compatibility (until device support is added into the framework and linux by the development team), but will come with every feature.

The Grey/Orange (brick decorated) USB Adapters are functionally the same, after using the latest firmware. Gamepads may switch to different input modes using hotkeys for different functionality (depends upon the model of controller, some have a switch on the back like the 8bitdo SN30 Pro 2). Note that documentation on 8Bitdo's site doesn't specify this, but the update logs for the firmware updates does.

* X-Input mode: Hold SELECT+UP for 3 seconds.
* PSC (Playstation Classic) mode: Hold SELECT+DOWN for 3 seconds. This is useful for gamepads which are limited in buttons (12 total; DPAD counts as 4) and need to access the MiSTer OSD menu. Note that the OSD menu should not be assigned when configuring buttons in the main MiSTer menu core, as the L+R+START combination will bring up the OSD while in the cores. The combination is hard-coded in MiSTer specifically for 8Bitdo adapters. You may also lose auto-fire/mouse functionality in this mode.

Alternative 8Bitdo adapters, such as the 8Bitdo Console Retro Receiver (SNES, NES, Genesis) are always in X-Input mode when connected via microUSB.
