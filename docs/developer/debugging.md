While developing the core, it's convenient to upload it through USB blaster(JTAG) port directly from Quartus. MiSTer supports USB Blaster and automatically reloads Linux part for uploaded core. Since Linux requires reboot (for better stability), you may notice longer time to start the core. This is normal. It's advised to have console connected to MiSTer to control the booting process. Once core compiled in RBF format and put into SD card, loading speed will be fast.

## Configuring USB Blaster on Linux
Although there is no need for drivers on linux, by default only root user can access the cable. In order to use it as a regular user just add a file called `/etc/udev/rules.d/92-usbblaster.rules` with the following content:

```
# USB-Blaster 
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6001", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6002", MODE="0666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6003", MODE="0666"

# USB-Blaster II
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6010", MODE="666"
SUBSYSTEM=="usb", ATTR{idVendor}=="09fb", ATTR{idProduct}=="6810", MODE="666"
```
