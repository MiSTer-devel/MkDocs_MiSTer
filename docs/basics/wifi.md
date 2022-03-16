---
hide:
  - toc
---

Wifi is totally optional and it's setup is fairly simple with the MiSTer. You will need a compatible dongle, the wifi script (which is provided with the Mr. Fusion image), and a keyboard attached to your MiSTer to type in your WiFi password.

## Suggested WiFi Adapters

You will require a compatible USB WiFi Adapter to use this feature as there is no integrated WiFi on the DE10-Nano or the MiSTer Add-on boards. Not all models of wifi adapters are compatible, so try to stick with decent name brands. Many users have found that most small ASUS, TP-Link, CanaKit, and Edimax wifi USB adapters work out of the box. Here's a few that have been reported to work:

* ASUS USB AC53 nano rev A1
* TP-Link AC1300 Archer T3U or Nano AC600 Archer T2U
* CanaKit Raspberry Pi WiFi dongle
* Edimax EW-7612UAn v2 or EW-7811UN or EW-7822ULC
* Netgear A6100 or A6150

Your results may vary as there may be new hardware revisions of these adapters which are not currently supported. There are ways to compile your own drivers for your device but that is for advanced users. **INSERT LINK TO NEW DOC FOR THIS**

## Setup wifi with a script

It's easy to connect to WiFi using the wifi.sh script provided with the Mr. Fusion image:

1. Navigate to the scripts menu using the on screen display (OSD). 
2. Select the "wifi" script and run it.
3. Select your WiFi network's SSID (the name of your WiFi). 
4. Type your WiFi password in and press enter.
5. It should connect and ask you to press any key to continue. 

At the top of the main menu you will see a little wifi icon which indicates you have connected. This setting should be saved and it will automatically connect so long as the adapter is plugged in and your MiSTer is within range of your WiFi network.

## The manual way to setup wifi

In case the script isn't working for you, you can try to manually setup Wifi. This is a slightly more advanced user method so feel free to ask for help from the community before attempting this method. To manually setup WiFi without the script:

1. Edit the file `/media/fat/linux/_wpa_supplicant.conf` with a text editor that supports Unix/Linux line endings.
2. Replace `put_your_SSID_here` with your Wifi Network's SSID, and replace `put_your_password_here` with your WiFi password. 
3. Change the country code [to the one that matches your country](https://www.arubanetworks.com/techdocs/InstantWenger_Mobile/Advanced/Content/Instant%20User%20Guide%20-%20volumes/Country_Codes_List.htm){target=_blank}. 
4. Rename `_wpa_supplicant.conf` to `wpa_supplicant.conf`
5. Reboot the MiSTer.

After the MiSTer reboots you should see the wifi icon at the top of the Main Menu's OSD. This may take quite awhile so be patient, the MiSTer is not very fast at connecting to your WiFi network, it's a simple device with simple capabilities.
