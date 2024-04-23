There are many computer-core specific features and functionality to go over. Here are a few:

# Computer core Internet and console connections

Starting from 2018 may 7 release MiSTer supports serial (UART) connection from FPGA to Linux. Linux OS runs PPP or Console daemon on this connection allowing access the internet or Linux shell from FPGA cores.

## Cores supporting serial connection

* **Minimig**. Tested on [Roadshow TCP/IP](https://misterfpga.org/viewtopic.php?f=4&t=2063&p=18598&hilit=Roadshow#p18598){target=_blank}, AmiTCP and Miami. 
    1. AmiTCP provides more complete solution with ftpd daemon. There are many other 3rd party addons are based on AmiTCP, so it's advised to use this package.
    2. Roadshow works very well, it is fully compatible with AmiTCP and offers additional extensions. Follow these [Instructions](https://misterfpga.org/viewtopic.php?f=4&t=2063&p=18598&hilit=Roadshow#p18598){target=_blank} for complete setup.  It is still a paid for and supported product, you can find more information [here](http://roadshow.apc-tcp.de/index-en.php){target=_blank}.
    3.  Miami was successfully tested. The Miami settings that worked: use PPP connection via serial.device, set baud rate to 115200, RTS/CTS to on, and enable 8N1. Set modem to nullmodem. Manually enter an IP suitable for your lan ending in 254, e.g. 192.168.1.254. Manually add a DNS server, e.g. 8.8.8.8 for Google DNS. Term v4.7 has been used to test console connection. For a more detailed MiamiDX setup guide, please check [here](https://www.geocities.ws/allforamiga/){target=_blank}
    4.  You can also double the speed on Minimig by modifying the /sbin/uartmode script, like mine:
```sh
echo "$localip:$remoteip" >/tmp/ppp_options
cat /media/fat/linux/ppp_options >>/tmp/ppp_options

echo 1 > /proc/sys/net/ipv4/ip_forward
[ -f /tmp/CORENAME ] && core_name=$(cat /tmp/CORENAME)
    if [ "$core_name" == "Minimig" ]; then
        taskset 1 pppd 230400 file /tmp/ppp_options
    else
        taskset 1 pppd $conn_speed file /tmp/ppp_options
    fi
```
Of course, change the baud rate as well to 230400 on your TCP/IP stack of choice. Tested under MiamiDX, no issues.

* **ao486**. PPP and serial connections are working under DOS, tested with mTCP and various terminal software. PPP is also working under Win3.11/Win95/Win98/NT 4.0.
DOS tools are here : [dos_ftpd.zip](https://github.com/MiSTer-devel/ao486_MiSTer/raw/master/sw/dos_ftpd.zip){target=_blank}. The DOS FTP server included does not support passive mode, so set your client to use active.
* **PC XT**. PPP and serial connections are working under DOS, tested with mTCP/DOS PPP and various terminal software.
* **C64**. Serial connection.
* **Tandy Color Computer 3 (CoCo3)**. Serial Connection.
* **Macintosh Plus**. Serial and PPP support.
* **AtariST**. Serial and PPP support.
* **Apple IIe**. Serial Connection

OSD provides an option to switch between PPP and Console on these cores.
Both console and PPP are using baud rate 115200 8N1 mode with hardware RTS/CTS flow control for stability.

## Console connection

Using this connection with supported terminal application on FPGA core, you can access the Linux shell and do some file managements or Linux settings if required.

No special settings are required of Linux. 

## PPP connection

Using this connection core may have internet connection. More important, the core may run ftp daemon and provide access to its filesystem, so you can use FTP client on PC to move the files to/from the emulated system.

PPP daemon uses **/media/fat/linux/ppp_options** (linux\ppp_options of PC) file. Most likely you don't need to modify it. Recent update assigns IPs automatically. **Core gets <your_net>.254 IP (for example 192.168.1.254). If you want to use other IP or your router has the .254, then modify ppp_options file.**. At the bottom of the file uncomment and modify the last line:
```ini
# You may explicitly define local and remote IPs for PPP link.
# new MiSTer releases don't require it anymore.
# IPs entered here will override automatically assigned IPs.
#192.168.1.1:192.168.1.10
```

For correct PPP work, make sure you see a network icon in Menu core before starting the other core. Otherwise PPP link won't get IPs. If you've started core earlier, then simply connect the core to PPP and disconnect. Next connection will get correct IP. Or you can switch UART mode in OSD to renew the IP.

## PPP connection in MS-DOS on ao486

1. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "PPP", Baud to "115200" and save it.
2.  Download the DOS PPPD driver: DOSPPP06.ZIP from [HERE](https://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/net/dosppp/){target=_blank}.
3.  Grab the latest version of Michael Brutman's mTCP TCP/IP applications for MS-DOS, from the 'Downloads' section [HERE](http://www.brutman.com/mTCP/){target=_blank}
4.  Transfer those zip files over to your ao486's virtual hard drive and unzip them into the directory of your choice (e.g. C:\NETWORK)
5.  In MS-DOS on the core, you need to edit a mtcp config file. There's a sample config in the SAMPLES directory called 'sample.cfg' that you can use as a base, 
or you can use the example below (simple text file named mtcp.cfg in your installation folder). If you use the sample.cfg file, you need to add the top MTCPSLIP line.:
```ini
SET MTCPSLIP=true
mtu 1500
packetint 0x60
hostname ao486_fpga
IPADDR 192.168.1.254 <- Change this to reflect your network. Only the first three octets (e.g. 192.168.1), the last .254 is the default IP assigned to the core !!!
NETMASK 255.255.255.0
GATEWAY 192.168.1.1 <- Change this to reflect your network.
NAMESERVER 8.8.8.8 <- You can change this to reflect your network if you want to.
LEASE_TIME 86400
IRCJR_USER FPGA_User
IRCJR_NICK fpga_user
IRCJR_NAME FPGA_User
```
6. Edit your AUTOEXEC.BAT and add the path to your installation folder, as well with the MTCP variable:
```bat
PATH C:\DOS;C:\NETWORK
SET MTCPCFG=C:\NETWORK\MTCP.CFG
```
7. The DOS PPPD driver archive includes the ppp packet driver, which you need to load:
```bat
epppd com1 115200 local
```
8. Enjoy telnet, ftp, irc, and other internet applications while you use MS-DOS. Be sure and make sure you have ANSI.SYS loaded in CONFIG.SYS if you want to use the telnet client to hit telnet BBSes. Original discussion [HERE](https://misterfpga.org/viewtopic.php?t=896){target=_blank}.

## PPP connection in Windows 3.11 on ao486

1. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "PPP", Baud to "115200" and save it.
2. Get the Trumpet Winsock PPP client
    * Download the software.  There are other newer versions available BUT be warned only version 3.0 will work.
        * [Trumpet Winsock 3.0](https://winworldpc.com/product/trumpet-winsock/3x){target=_blank}
3. License the Software - This software is still shareware (time limited) please license it appropriately. Once you acquire a license you can put the details in Tcpman in the "Special" menu in "Password registration"
4. Configure Software  
    * Start Tcpman
    * Under File-->PPP Options ensure all checkboxes are unchecked and the text boxes are blank.
    * Under File-->Setup Enter an "IP Address" suitable for your LAN eg 192.168.1.254 and a "DNS Server(s)" 192.168.1.1
        * Under the Driver section select the PPP radio button and click on "Dialer settings..."  
    * In the "Dialer settings..."  
        * "COMM port" COM1  
        * "Baud rate" 115200

## PPP connection in Windows 95/98 on ao486

1. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "PPP", Baud to "115200" and save it.
2. Get the modem driver from [HERE](https://github.com/MiSTer-devel/ao486_MiSTer/blob/master/releases/drv/modem9x.inf){target=_blank} and transfer it to your VHD or a floppy image
    * Click the Windows 95 Start button, point to Settings, and then click Control Panel. Double-click Add New Hardware
    * Select No to Windows search for new harware. Click Next, then select Modem from next page.
    * Check "Don't detect my modem", then Have disk on the next page. Navigate to modem9x.inf location and install it.
3. Install Dial-Up Networking:
    * Click the Windows 95 Start button, point to Settings, and then click Control Panel. Double-click Add/Remove Programs.
    * Click the Windows Setup tab. Select Communications. Click Details, select Dial-Up Networking and click OK.
    * Click OK to close the Windows Setup dialog box. Now Dial-up networking should be now under "My Computer".
4. Create a dial-up connection
    * Open My Computer then Dial-Up Networking. Double-click on Make New Connection.
    * Name it to your liking, be sure to select Generic NULL Modem. Use any phone number you want, it won't matter. Hit Next then Finish to end setup
    * Right-click on the newly made connection, then Properties:
        * **General** tab - make sure the Generic Null Modem is selected and set to COM 1, 115200 baud
        * **Server Types** tab - Select "PPP: Windows 95, Windows NT 3.5, Internet" and Uncheck everything except TCP/IP
    * Hit OK, then double-click on thee dial-up connection to connect. You should have now a working PPP connection under Win95/98.
5. **Important:**
DNS is not acquired automatically by Windows 95 (or Windows NT) unless either:
    * Click on TCP/IP Settings in the above Server Types tab, TCP/IP Settings  and configure static name servers (either by using your router's internal IP address - usually .1 - or Google public ones like 8.8.8.8)
    * Login into your MiSTer by SSH or F9, go to /media/fat/linux and change your ppp_options file by uncommenting (delete the front #) and modifying the IP addresses from "ms-dns" entries:
```ini
# /etc/ppp/options

# Specify which DNS Servers the incoming Win95 or WinNT Connection should use
# Two Servers can be remotely configured
ms-dns 192.168.1.1  #CHANGE it to your network's needs
ms-dns 8.8.8.8         #or  8.8.4.4 etc
```

## PPP connection in Windows NT 4.0 on ao486

The full how-to install Windows NT 4.0 and PPP setup on [MiSTerFPGA forum](https://misterfpga.org/viewtopic.php?t=4400):

1. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "PPP", Baud to "115200" and save it. **Important: Plain 115200, not Turbo one !!!**
2. Get the modem driver from [HERE](https://github.com/MiSTer-devel/ao486_MiSTer/blob/master/releases/drv/modem9x.inf){target=_blank} and transfer it to your VHD or a floppy image
3. Mount Windows NT 4.0 CD-ROM image 
4. Open My Computer and click on the Dial-Up Networking. When prompted, navigate to /i386 folder on the CD-ROM. There will be the "rascfg" files and the rest needed for setup.
5. During setup, when **Remote Access Setup** asks you to add a modem, hit **Yes**, then in the following window, check **"Don't detect my modem..."**. In the next window, click on **"Have disk"** and point to where modem9x driver is.
6. From that point on, the setup will take you to use the **Generic null modem**, hit **OK**, hit **Continue**, check only **TCP/IP** when prompted then again **Continue**. Setup will continue and at some point it will ask you to restart.
7. After installing Dial-Up Networking, you will get an Event Error at every boot. It doesn't break PPP, but get rid off it by re-running the Service Pack 6 (mount misternt.iso CD-ROM and run sp6ai386) and restart again when asked.
8. The New Phonebook Entry Wizard will appear after, name your connection to your liking and Check "I know all about phonebook...." box to jump to finish. You can use any number (I used 555-1234).
9. Click on **More** then **Edit entry and modem properties**
    * **Basic** tab - be sure to  have "Dial using" set to Generic NULL modem (COM1), speed set to 115200
    * **Server** tab - uncheck everything except TCP/IP, Dial up server type should be "PPP: WinNT, 98 Plus, Internet"
10. **Important:**
DNS is not acquired automatically by Windows NT (or Win95) unless either:
    * Click on TCP/IP Settings in the above Server tab and use configure static Nameserver (either by using your router's internal IP address - usually .1 - or Google public ones like 8.8.8.8)
    * Login into your MiSTer by SSH or F9, go to /media/fat/linux and change your ppp_options file by uncommenting (delete the front #) and modifying the IP addresses from "ms-dns" entries:
```ini
# /etc/ppp/options

# Specify which DNS Servers the incoming Win95 or WinNT Connection should use
# Two Servers can be remotely configured
ms-dns 192.168.1.1  #CHANGE it to your network's needs
ms-dns 8.8.8.8         #or  8.8.4.4 etc
```

## PPP connection in MS-DOS on PC XT

Instructions would be the same as for DOS under ao486, the only difference is that the PPP connection will use COM 2 serial port on the XT core, instead of COM 1 as on ao486:
1. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "PPP", Baud to "115200" and save it.
2.  Download the DOS PPPD driver: DOSPPP06.ZIP from [HERE](https://www.ibiblio.org/pub/micro/pc-stuff/freedos/files/net/dosppp/){target=_blank}.
3.  Grab the latest version of Michael Brutman's mTCP TCP/IP applications for MS-DOS, from the 'Downloads' section [HERE](http://www.brutman.com/mTCP/){target=_blank}
4.  Transfer those zip files over to your PC XT's virtual hard drive and unzip them into the directory of your choice (e.g. C:\NETWORK)
5.  In MS-DOS on the core, you need to edit a mtcp config file. There's a sample config in the SAMPLES directory called 'sample.cfg' that you can use as a base, 
or you can use the example below (simple text file named mtcp.cfg in your installation folder). If you use the sample.cfg file, you need to add the top MTCPSLIP line.:
```ini
SET MTCPSLIP=true
mtu 1500
packetint 0x60
hostname PCXT_fpga
IPADDR 192.168.1.254 <- Change this to reflect your network. Only the first three octets, the last .254 is the default IP assigned to the core !!!
NETMASK 255.255.255.0
GATEWAY 192.168.1.1 <- Change this to reflect your network.
NAMESERVER 8.8.8.8 <- You can change this to reflect your network if you want to.
LEASE_TIME 86400
IRCJR_USER FPGA_User
IRCJR_NICK fpga_user
IRCJR_NAME FPGA_User
```
6. Edit your AUTOEXEC.BAT and add the path to your installation folder, as well with the MTCP variable:
```bat
PATH C:\DOS;C:\NETWORK
SET MTCPCFG=C:\NETWORK\MTCP.CFG
```
7. The DOS PPPD driver archive includes the ppp packet driver, which you need to load:
```bat
epppd com2 115200 local
```

## Serial connection on C64

The following is an example for connecting to a BBS using Striketerm 2014 and VIC-101 2400 baud mode:

1. Start the C64 core (please note that custom kernels may remove functionality required, if in doubt use the built in kernel).
2. In the Mister C64 Menu ++win+f12++ , go to "Hardware", set the "Expansion" to "RS232", "RS232 Connection" to "Internal", "RS232 mode" to "VIC-1011" and save it.
3. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "Modem", Link to "TCP", Baud to "2400" and save it.
4. Load Striketerm 2014 from d64. Available from [here](https://csdb.dk/release/?id=130807){target=_blank}
5. Keep the defaults in the Main Menu ++f1++ , ensure you are running at 2400 baud.
6. Save a BBS into the Addressbook ++f5++, you can get some from [here](http://cbbsoutpost.servebbs.com){target=_blank}
7. Surf the BBS very slowly...

The following is an example for connecting to a BBS using CCGMS Ultimate and UP9600 mode:

1. Start the C64 core (please note that custom kernels may remove functionality required, if in doubt use the built in kernel).
2. In the Mister C64 Menu ++win+f12++ , go to "Hardware", set the "Expansion" to "RS232", "RS232 Connection" to "Internal", "RS232 mode" to "UP9600" and save it.
3. In the Mister System Menu ++win+f12++ set the "Uart Connection" to "Modem", Link to "TCP", Baud to "9600" and save it.
4. Load CCGMS Ultimate from d64, available [here](https://csdb.dk/release/download.php?id=214853){target=_blank}
5. Hit ++f7++ key to access configuration page, then ++m++ to change the modem to "UP9600/EZ232", then ++b++ to set the baud speed to "9600". Save the config with the ++s++ key.
6. Access the Phonebook with ++a++ key from the same configuration page, save some BBS addresses from [here](http://cbbsoutpost.servebbs.com){target=_blank}
7. Enjoy the faster BBS experience.

## Serial connection on Color Computer 3 (CoCo3)

The following is an example for connecting to a BBS using UltimaTerm 4.0:

1. Start the CoCo3 core (use Multi-pak Slot 4 Disk or Slot 2 CoCoSDC)
2. In the MiSTer System Menu ++win+f12++  set the "Uart Connection" to "Modem", Link to "TCP", Baud to "9600" and save it.
3. Mount UltimaTerm DSK file, obtainable [HERE](https://colorcomputerarchive.com/repo/Disks/Applications/Ultimaterm%204.0%20%28Ken%20Johnston%29%20%28Coco%203%29.zip){target=_blank}
4. Load UltimaTerm by issuing: `LOADM"ULTIMATE`
5. Hit ++alt+o++ to open Options Menu, then ++m++ for Modem options. Use ++b++ to modify the baud rate (++left++ or ++right++ arrows to change values) to 9600. The rest of the settings should be default (word length 8, parity none, stop bits 1, duplex full, terminal type ANSI). 
6. Save your changes with ++alt+d++ then ++f1++ key.
7. Hit ++alt+a++ to open Phonebook, add a BBS and dial away.
8. Alternatively, you can dial directly by issuing an `ATDTBBS_Address:port`. Full UltimaTerm 4.0 Documentation [HERE](https://colorcomputerarchive.com/repo/Documents/Manuals/Applications/Ultimaterm%20v4.0%20%28Ken%20Johnston%29.pdf){target=_blank}

## Serial connection on Apple IIe

Apple IIe has serial support via implemented SuperSerial Card in Slot 2. While theoretically some programs may use up to 19200 baud, I found it to be more stable at 1200 and/or 2400 baud.

Terminal programs tested:

* ACT - Apple Conference Terminal v.3.0.3 [HERE](https://mirrors.apple2.org.za/ftp.apple.asimov.net/images/communications/Apple%20Conference%20Terminal%20V3.0.3.dsk){target=_blank}
* Practical Peripherals Communication Program for Apple II v.1.01 [HERE](https://mirrors.apple2.org.za/ftp.apple.asimov.net/images/communications/Apple_II_Comm_Program.dsk){target=_blank}

1. Start the Apple IIe core
2. In the MiSTer System Menu ++win+f12++  set the "Uart Connection" to "Modem", Link to "TCP", Baud to "1200" and save it.
3. Load either of terminal programs listed above, both have intuitive menus and 80 column modes
4. Configure the terminal's baud speed to match the one set earlier (e.g. 1200 baud, Word Length 8, Stop Bits 1, Parity None, SuperSerial Card Slot 2)
5. Enter in terminal mode and ATDT your favorite BBS
