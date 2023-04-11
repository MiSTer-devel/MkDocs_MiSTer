Bluetooth adapters and using controllers over bluetooth is supported on the MiSTer.

## Compatible adapters

Generally speaking, most bluetooth 4.0 adapters use one of two similar chips, the CSR8510 and the BCM20702, and these are compatible. Bluetooth 5.0 adapters are a little different, but many are compatible as well. Here is a list of a few known compatible adapters:

* [ASUS USB-BT500 (5.0)](https://www.amazon.com/dp/B08DFBNG7F){target=_blank}
* [Edimax BT-8500 (5.0)](https://www.amazon.com/Edimax-BT-8500-Bluetooth-Supports-Controllers/dp/B08M1VJHVD/){target=_blank}
* [MiSTerAddons.com's Bluetooth 4.2 / WiFi AC600 Combo Adapter](https://misteraddons.com/collections/parts/products/wifi-bt-usb-adapter){target=_blank}
* [MiSTerFPGA.co.uk's CSR8510 Bluetooth 4.0 Adapter](https://misterfpga.co.uk/product/mister-fpga-bluetooth-adapter-dongle/){target=_blank}
* [MiSTerKits.com's CSR8510 Bluetooth 4.0 Adapter](https://www.misterkits.com/products/mister-bluetooth-adapter){target=_blank}
* [ZEXMTE Long Range USB Bluetooth (5.0)](https://www.amazon.com/ZEXMTE-Bluetooth-Adapter-Keyboard-Headphones/dp/B09D7W918Q){target=_blank}

There are many more that work than these few. Please note that some hardware revisions may change the compatibility of even the adapters in this list, your results may vary. For the most part, most adapters seem to work fine.

## How to pair your Bluetooth controller or Keyboard

This is the easy part. Simply press the ++f11++ key on a keyboard that is already connected to the MiSTer and the pairing prompt will pop up. Alternatively, if you have a Digital IO or Analog IO addon board, then you can press and hold the OSD button to bring up the same bluetooth pairing prompt. Put your controller into pairing mode and wait. The MiSTer should find it momentarily and connect to it. You may need to define your inputs for this new controller, even if it's been plugged directly into the MiSTer before as it is seen as a different controller over bluetooth.

## Bluetooth connection to MiSTer unstable?

If your bluetooth connection to the MiSTer is unstable (e.g. losing the connection to your controller randomly), try getting a usb extension / pigtail adapter to move the adapter away from the USB hub. For some people the USB hub can add interference and can interrupt some adapters (like the ASUS USB-BT500 in some cases). The root cause of this behavior is not currently known.
