There are multiple advanced networking features that the MiSTer can utilize. Here we will go over quite a few of them.

## CIFS Share Mounting
The MiSTer can mount a network share from another computer or server as if it were storage. There are two scripts that are used by the MiSTer for CIFS mounting and unmounting.

[cifs_mount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_mount.sh){target=_blank}

This script mounts the desired network share to the MiSTer in such a way that any identical folders from `/media/fat` will be put on a lower priority and you will see the ones from the network share in place of the ones on your MicroSD. See [Core Paths](../cores/paths.md) for more specific information as to how this hierarchy functions.

[cifs_umount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_umount.sh){target=_blank}

This script will unmount the network share when ran.

## RetroNAS
A project was launched that makes it easier to get a network attached storage (NAS) device up and running which was focused solely on retro gaming device compatibility. The MiSTer was one of their primary focuses and it works quite well. All you need is a Raspberry Pi4 and some kind of external hard drive storage device. Remember: NAS IS NOT BACKUP! You could lose data if you rely solely on a NAS for important data. They have a good [installation guide](https://github.com/danmons/retronas/wiki/Installing-RetroNAS){target=_blank} that is simple to follow and [MiSTer-specific instructions](https://github.com/danmons/retronas/wiki/MiSTer-FPGA){target=_blank} to help get you started. They also have video guides available on Youtube for [installation](https://www.youtube.com/watch?v=szA-MSabplc){target=_blank} and [MiSTer FPGA-specific configuration](https://www.youtube.com/watch?v=OrTctA-5kqk){target=_blank} if you prefer.

## Static IP Address configuration
Currently the best way to do this is using `connmanctl` (try `connmanctl help` for more info).
* Create /var/lib/connman directory so changes will persist across reboots  
```
# mkdir /var/lib/connman
```
* Find your on-board network service name.  
```
# connmanctl services
*AO Wired                ethernet_020304050607_cable
```
* Setup IP address (e.g. `192.168.1.123`, should be unused), subnet mask (e.g. `255.255.255.0`) and gateway (e.g. `192.168.1.1`, typically your router IP address). To configure the right device use the service name returned from above command (e.g. `ethernet_020304050607_cable`). This will disable the use of DHCP.  
```
# connmanctl config ethernet_020304050607_cable --ipv4 manual 192.168.1.123 255.255.255.0 192.168.1.1
```
* Setup one or more DNS server(s) (e.g. `192.168.1.1` from your router, `8.8.8.8` from Google DNS.  
```
# connmanctl config ethernet_020304050607_cable --nameservers 192.168.1.1 8.8.8.8
```
You could write a script to help with typing and remembering your settings.

> You can also setup your on-board network connection by editing `/etc/network/interfaces`. This is currently not advised. Because if you have a DHCP server in your network, the network stack will still contact the DHCP server and assign the returned IP address regardless, leading to usually unwanted behavior.

## Re-Enabling DHCP
```
# connmanctl config ethernet_020304050607_cable --dhcp
```