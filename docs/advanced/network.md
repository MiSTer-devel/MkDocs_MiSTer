There are multiple advanced networking features that the MiSTer can utilize. Here we will go over quite a few of them.

## Network access
MiSTer board can be access through on-board Ethernet port. System has **FTP**, **SSH**, **SFTP** services running.

User name: **root**  Password: **1**

When using FTP, make sure your file transfers are in Binary not ASCII. ASCII-type transfers will result in corruption of that data. A good FTP client for Windows that defaults to Binary and supports FTP as well as SFTP and SCP (ssh copy) is [WinSCP](https://winscp.net/eng/download.php).

## Share Mounting
The MiSTer can mount a network share from another computer or server as if it were storage. CIFS and NFS shares are supported. The following helper scripts are provided to simplify this process, if you want to use them download to them to /media/fat/Scripts

### CIFS mounting and unmounting

[cifs_mount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_mount.sh){target=_blank}

This script mounts the desired network share to the MiSTer in `/media/fat/cifs`  MiSTer will give preference to the folders mounted in that path. See [Core Paths](../cores/paths.md) for more specific information as to how this hierarchy functions.

[cifs_umount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_umount.sh){target=_blank}

This script will unmount the network share when ran.

### NFS mounting and unmounting.

[nfs_mount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/nfs_mount.sh){target=_blank}

This script mounts the desired network share to the MiSTer in such a way that any identical folders from `/media/fat` will be put on a lower priority and you will see the ones from the network share in place of the ones on your MicroSD. See [Core Paths](../cores/paths.md) for more specific information as to how this hierarchy functions.

[nfs_umount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/nfs_umount.sh){target=_blank}

This script will unmount the network share when ran.

### CIFS Share Troubleshooting
There is a known problem with certain cores (ao486 and NeoGeo, at least) and certain CIFS Share configurations, caused by [some open bugs](https://bugzilla.samba.org/show_bug.cgi?id=12783) in Samba.

If certain cores doesn't start when loading games from CIFS share but work OK when loading from SD or USB, check if Kernel Oplocks are enabled on the CIFS share. If they are, either disable them, enable them globally on your Samba server, or move your MiSTer files to a different share exclusively used for MiSTer and without Kernel Oplocks enabled. It is up to you to decide which one fits better your use case: Kernel Oplocks are enabled by default in many NAS for good reason, as this should prevent bad file synchronization, corruption, and data loss when the shared folder is used by different protocols (i.e. CIFS and NFS) or by network clients and software running in the NAS like a torrent client.

## RetroNAS
A project was launched by Dan Mons that makes it easier to get a network attached storage (NAS) device up and running which was focused solely on retro gaming device compatibility. The MiSTer platform is one of the project's primary focuses and it works quite well. All you need is a Raspberry Pi4 or Pi5 and some kind of external hard drive storage device. Remember: NAS IS NOT BACKUP! You could lose data if you rely solely on a NAS for important data. They have a good [installation guide](https://github.com/danmons/retronas/wiki/Installing-RetroNAS){target=_blank} that is simple to follow and [MiSTer-specific instructions](https://github.com/danmons/retronas/wiki/MiSTer-FPGA){target=_blank} to help get you started. They also have video guides available on Youtube for [installation](https://www.youtube.com/watch?v=szA-MSabplc){target=_blank} and [MiSTer FPGA-specific configuration](https://www.youtube.com/watch?v=OrTctA-5kqk){target=_blank} if you prefer.

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

## Tailscale Networking

Adding your MiSTer to a Tailnet has a lot of benefits: being able to travel with it while still retaining access to a NAS with games hosted on it, being able to remotely administer a less-technical friends MiSTer and being able to remotely SSH/SFTP in to your MiSTer to run scripts and install cores to name a few.

If you do not already have a Tailnet, follow the instructions [here](https://tailscale.com/kb/1017/install){target=blank} to get started. Make sure you add at least one computer/NAS/phone to the Tailnet once it's created.

Go to the [Tailscale Package Repository](https://pkgs.tailscale.com/stable/#static){target=blank} and download the ARMv7 binary package (It will look something like `arm: tailscale_x.xx.x_arm.tgz`).

Extract the archive on your computer and SFTP the files (`tailscaled` and `tailscale`) to your MiSTer. In this documentation we use the path `/media/fat/linux/tailscale/` but you can use any directory under `/media/fat/` just make sure you edit all the paths in the examples and scripts that follow.

SSH into your MiSTer and change directory to where you put the extracted Tailscale files. Create a directory to house the Tailscale state on boot with `mkdir .state`. Now start the Tailscale Daemon with the following command:
```
# /media/fat/linux/tailscale/tailscaled --tun=userspace-networking --statedir=/media/fat/linux/tailscale/.state/
```
`--tun=userspace-networking` is added because the MiSTer Linux Kernel is not compiled with TUN support, so running it in the userspace allows the daemon to start. `--statedir=/media/fat/linux/tailscale/.state/` is to prevent the daemon from erroring out on a cold boot when the OS root directory is mounted as Read Only.

Once the Dameon starts, you can then run the the following command to get your MiSTer joined to your tailnet:
```
# /media/fat/linux/tailscale/tailscale up --accept-routes
```
The `--accept-routes` is only needed if you have a machine on your tailnet set up as a subnet router.

When that command finishes you will see a URL at the bottom of it's output. This is the URL that you will need to paste into your browser to join the device to your Tailnet. Do that now.

Once you have the MiSTer joined to the Tailnet, create a `tailstart.sh` file in the tailscale directory and put the following into it (with your preferred command line editor):
```
#/bin/sh

/media/fat/linux/tailscale/tailscaled --tun=userspace-networking --statedir=/media/fat/linux/tailscale/.state/ > /dev/null 2>&1 &
/media/fat/linux/tailscale/tailscale up --accept-routes > /dev/null 2>&1 &
```

Once the file is created and has the script in it, run:
```
# chmod +x tailstart.sh
```
Now to have Tailscale start when your MiSTer boots, edit the `user-startup.sh` file in `/media/fat/linux/` and add the following line to the bottom of it:
```
/media/fat/linux/tailscale/tailstart.sh
```

Now your MiSTer will connect to your Tailnet after every reboot.
