## The MiSTer FPGA's correct DIP switch configuration on the DE10-Nano

If your keyboard doesn't work or something else low-level hardware related doesn't work, it's possible that one or more of the DIP switches on your DE10-Nano are misconfigured. Make sure the DIPS are configured like the following pictures:  
![MiSTer FPGA DIP Switches Correct Configuration - Small DIPS - Terasic DE10-Nano](img/dips1.png)  
![MiSTer FPGA DIP Switches Correct Analog IO board Configuration - Big DIPS - Terasic DE10-Nano](img/dips2.png)

Side Note: If you have a Digital IO board then your first of the large dips in the 2nd picture above needs to be turned On (up) and the rest should be turned off (down) in order to use the 2nd SDRAM module, if you have one. Here's a demonstration with a picture again:  
![MiSTer FPGA DIP Switches Correct Digital IO board Configuration - Big DIPS - Terasic DE10-Nano](img/dips3.png)  
*Credit for 2nd and 3rd pictures goes to Nat from [MiSTerFPGA.co.uk](https://misterfpga.co.uk){target=_blank}*

| Board      | SW0 | SW1 | SW2 | SW3 |
| ---------- | --- | --- | --- | --- |
| Analog IO  | Off | Off | Off | Off |
| Digital IO | Off | Off | Off | On  |

## My gamepad doesn't work

If your gamepad doesn't work in the menu, you need to make sure you have [defined your inputs for that gamepad](../setup/controller.md){target=_blank}. If your gamepad doesn't work in the core, but it does work in the menu, then you need to define the gamepad in that core in the secondary OSD menu. If neither of these work, make sure you your DIP switches are correct as shown above.

## My Keyboard doesn't work right

If you have a fancy gamer keyboard with lots of macros and RGB lights, it's possible that the stock power supply is not providing enough power. You may want to consider purchasing an upgraded power supply with more amps as a way to fix this, like the [Mean Well GST18A05-P1J](https://www.amazon.com/MEAN-WELL-GST18A05-P1J-Desktop-Adaptor/dp/B01LZ0LJXQ){target=_blank} or take a look at this [DigiKey search result](https://www.digikey.com/short/33rwd9pm) to get a better idea of what is required. Generally speaking you need a 5v power supply with more than the stock 2amps, with a 2.1mm x 5.5mm x 11.0mm barrel plug that has positive center polarization. Mean Well and Triad are often recommended brands, but they are not the only option if you cannot find them at your desired retailer.

## Fixing missing certs

If you are unable to use wget, this might be because you are missing security certificate files. The default system comes with no security certificate files so you need to add --no-check-certificate on wget to download anything HTTPS:

1. Open the linux terminal/command prompt with F9, use `root` as your username and `1` as your password.
2. Type `cd /etc/ssl/certs` and press enter.
3. Type `cp cacert.pem cacert.pem.bak` to make a backup of your existing cert.
4. Type `wget --no-check-certificate https://curl.se/ca/cacert.pem -O cacert.pem` and press enter.

Assuming it downloaded correctly, you can _now_ use wget as nature intended.

## WiFi shows two ip addresses and no internet connection

If you have no Internet connection to the MiSTer (you can't update the MiSTer, for instance), and you run ip addr and your wlan0 device shows two IP addresses, that might be the root of your problem. Some WiFi adapters seem to show this behavior, even on regular linux computers, the actual root cause is not fixable. You will not have internet access in many cases if one of the two addresses is an "APIPA" address (e.g. 168.254.xxx.xxx). To temporarily clear this problem run the following command from the terminal:

`ip addr flush wlan0`

It may come back again when your local DHCP server's lease is up and new IP addresses are received. In most home networks your dhcp server is your Router/Modem combo unit.

## Fixing a corrupted linux image on the MiSTer

Sometimes MicroSD cards may corrupt data over time, this is normal. Rarely this can result in the linux files on the MiSTer becoming corrupted. If you notice any low-level hardware related problems like the following (but not limited to):

* HDMI video output not working anymore
* USB controllers and even keyboards not working
* Internet no longer working anymore
* Sound not working over HDMI anymore
* WiFi not working anymore

And many more potential hardware failures... Then it is best to try and redownload the linux files and overwrite them. The best way to do this is by following these instructions:

1. Remove the MicroSD card from your MiSTer and insert it into your PC.
2. Download the latest sd-installer release archive (usually in .7z format at the bottom of the list) from here --> [https://github.com/MiSTer-devel/SD-Installer-Win64_MiSTer](https://github.com/MiSTer-devel/SD-Installer-Win64_MiSTer){target=_blank} and unzip it on your PC.
3. Copy and overwrite the contents of the linux folder from the archive you just downloaded over the linux folder on your MiSTer MicroSD.

This is essentially what a "Linux Update" does when you run the update script. This should get everything back to normal defaults. You may need to do the [WiFi setup](wifi.md) steps again if you are using WiFi.
