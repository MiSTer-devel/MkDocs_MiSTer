There are multiple advanced networking features that the MiSTer can utilize. Here we will go over quite a few of them.

## Network access
MiSTer board can be access through on-board Ethernet port. System has **FTP**, **SSH**, **SFTP** services running.

User name: **root**  Password: **1**

### FTP/SFTP
The File Transfer Protocol (FTP) is a standardized network protocol that allows computers on a network to transfer files between each other. 
It can be used to upload or download files to your MiSTer from another computer on the network without having to remove the SD card.
SFTP is simply FTP with an encrypted connection, however; it should be noted that not all FTP clients support SFTP.

You can use whatever FTP or SFTP client you prefer
so long as you make sure your file transfers are in binary and not ASCII.
ASCII-type transfers will result in corruption of that data.

Once connected to the MiSTer your SDCard content will be in the `/media/fat` path.

If you don't have a compatible FTP client already then try [FileZilla](https://filezilla-project.org/download.php?type=client){target=blank}. 
It is a solid choice for Linux, MacOS and Windows.
Another good FTP client for Windows is [WinSCP](https://winscp.net/eng/download.php){target=blank}.

### SSH
Secure shell (SSH) is a standardized network protocol for remotely operating computers over a network.
It can be used to operate a text terminals of computers (including the one on your MiSTer) remotely from another computer on the network.

On Linux and MacOS the `ssh` client is more than likely pre-installed. 
Open a terminal emulator and type `ssh` followed by the user and address. 
For example if the MiSTers IP address is `192.168.2.8` and you wanted to login as the `root` user,
then the command to connect would be `ssh root@192.168.2.8`.

There is no official SSH client for Windows but [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) can be used instead.
Using the same example as above type `root@192.168.2.8` into the **Host Name** text field.
Ensure **Port** is set to `22` and **Connection type** is set to **SSH** then click **Open**.

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
By default, MiSTer uses `dhcpcd` (not to be confused with `dhcpd`) to acquire a local network IP address from a DHCP server.
If you want to set a static IP address and/or router/DNS addresses.
You can do so by modifying `dhcpcd.conf`.
There are many other features available in `dhcpcd.conf` 
then what's discussed here. 
For full documentation read [dhcpcd.conf (5)](https://man.archlinux.org/man/dhcpcd.conf.5){target=blank}.

### Login to Linux terminal on the MiSTer
From the MiSTers startup menu, press ++F9++ to get a Linux terminal then
login as root (see [Network Access](#network-access) for the default credentials).

While you can use SSH to access the MiSTers Linux terminal remotely and configure a static IP address that way;
it is not recommended as you may lose network access (and therefore your SSH connection) to your MiSTer
after the IP address changes.

### Get the name of the network interface to assign a static IP address
There will always be at least two network interfaces on DE-10 Nano MiSTer:

| Interface Name | Description                                             |
|----------------|---------------------------------------------------------|
| `lo`           | Linux virtual network loopback device (not interesting) |
| `eth0`         | The DE-10 Nanos built-in Gigabit Ethernet               |

These two interface names should be consistent across all MiSTers.
However, if you want to set a static IP address on a USB network card, 
you will first need to know the name Linux has given to the interface.
To do this run the command `ip link` by typing it and then pressing ++Enter++.
You should get an output that looks somewhat like this:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
```
If necessary, you can run the command `ip addr` instead to see what IP address is currently assigned to each interface (if any).
You would get an output that looks somewhat like this:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 01:02:03:04:05:06 brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.221/24 brd 10.0.0.255 scope global dynamic noprefixroute eth0
       valid_lft 40368sec preferred_lft 34968sec
```
There will be an additional entry 
for each USB Wi-Fi and/or ethernet adapter MiSTer has recognized.
Take note of the interface name you want to change before proceeding to the next step.
The interface names are case-sensitive.

### Configure a static IP address to an interface

> Let's assume you want the network interface named `eth0` to be assigned a static ip address of `192.168.0.128`.
Replace these values with the network interface name you got in the previous step
and the IP address you want to set it to.

Open dhcpcd configuration file for editing by running the command `nano /etc/dhcpcd.conf` 
(or `vi /etc/dhcpcd.conf` if you know what that is and prefer it).
Press ++Down++ until you're at the bottom of the file then type the following:
```
interface eth0
static ip_address=192.168.0.128/24
```
Be sure to type these lines at the very bottom of the file as these lines are order-sensitive.
Any line below an `interface` line will apply to that interface until the next `interface` line.
Any line above the first `interface` line will apply to all network interfaces.

You can optionally specify any combination of options for an interface, here are some useful ones:

| Option                        | Description                                       |
|-------------------------------|---------------------------------------------------|
| `static routers=`             | Manually specify routers/gateways to the Internet |
| `static domain_name_servers=` | Manually specify DNS servers to revolve names     |
| `ntp_servers=`                | Manually specify NTP servers to get time from     |

With all these options manually specified a interface configuration could look somewhat like this:
```
interface eth0
static ip_address=192.168.0.128/24
static routers=192.168.0.1
static domain_name_servers=8.8.8.8 1.1.1.1
ntp_servers=192.168.0.1 0.pool.ntp.org 1.pool.ntp.org 2.pool.ntp.org
```

Once done, press ++Ctrl+o++ to make `nano` save `dhcpcd.conf` then ++Ctrl+x++ to exit `nano`.
Run the command `reboot` to restart the MiSTer back to the startup menu with the new network settings applied.

### Re-Enabling DHCP
If your static IP configuration isn't working, or you simply want to revert to automatic DHCP IP assignment.
Open `/etc/dhcpcd.conf` again and comment out the lines by placing a `#` character at the beginning of each line 
that you want to revert the behavior of.
Commenting out lines is as good as removing them but saves you having to write them again later if you change your mind.

To revert all of your configurations, comment out every line you added like so:
```
#interface eth0
#static ip_address=192.168.0.128/24
#static routers=192.168.0.1
#static domain_name_servers=8.8.8.8 1.1.1.1
#ntp_servers=192.168.0.1 0.pool.ntp.org 1.pool.ntp.org 2.pool.ntp.org
```
Just like before: save the file and reboot to restart the MiSTer
back to the startup menu with the new network settings applied.

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
