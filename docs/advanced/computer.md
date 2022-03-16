There are many computer-core specific features and functionality to go over. Here are a few:

# Computer core Internet and console connections

Starting from 2018 may 7 release MiSTer supports serial (UART) connection from FPGA to Linux. Linux OS runs PPP or Console daemon on this connection allowing access the internet or Linux shell from FPGA cores.

## Cores supporting serial connection
* **Minimig**. Tested on [Roadshow TCP/IP](https://misterfpga.org/viewtopic.php?f=4&t=2063&p=18598&hilit=Roadshow#p18598){target=_blank}, AmiTCP and Miami. 
    1. AmiTCP provides more complete solution with ftpd daemon. There are many other 3rd party addons are based on AmiTCP, so it's advised to use this package.
    2. Roadshow works very well, it is fully compatible with AmiTCP and offers additional extensions. Follow these [Instructions](https://misterfpga.org/viewtopic.php?f=4&t=2063&p=18598&hilit=Roadshow#p18598){target=_blank} for complete setup.  It is still a paid for and supported product, you can find more information [here](http://roadshow.apc-tcp.de/index-en.php){target=_blank}.
    3.  Miami was successfully tested. The Miami settings that worked: use PPP connection via serial.device, set baud rate to 115200, RTS/CTS to on, and enable 8N1. Set modem to nullmodem. Manually enter an IP suitable for your lan ending in 254, e.g. 192.168.1.254. Manually add a DNS server, e.g. 8.8.8.8 for Google DNS. Term v4.7 has been used to test console connection.
* **ao486**. Currently only console connection has been tested using Dos Navigator's integrated Terminal and Kermit 3.15. PPP should work under Win95.
DOS tools are here : [dos_ftpd.zip](https://github.com/MiSTer-devel/ao486_MiSTer/raw/master/sw/dos_ftpd.zip){target=_blank}. The DOS FTP server included does not support passive mode, so set your client to use active.
* **C64**. Serial connection.

OSD provides an option to switch between PPP and Console on these cores.
Both console and PPP are using baud rate 115200 8N1 mode with hardware RTS/CTS flow control for stability.

## Console connection
Using this connection with supported terminal application on FPGA core, you can access the Linux shell and do some file managements or Linux settings if required.

No special settings are required of Linux. 

## PPP connection
Using this connection core may have internet connection. More important, the core may run ftp daemon and provide access to its filesystem, so you can use FTP client on PC to move the files to/from the emulated system.

PPP daemon uses **/media/fat/linux/ppp_options** (linux\ppp_options of PC) file. Most likely you don't need to modify it. Recent update assigns IPs automatically. Core gets <your_net>.254 IP (for example 192.168.1.254). If you want other IP, then modify ppp_options file.

For correct PPP work, make sure you see a network icon in Menu core before starting the other core. Otherwise PPP link won't get IPs. If you've started core earlier, then simply connect the core to PPP and disconnect. Next connection will get correct IP. Or you can switch UART mode in OSD to renew the IP.

**NOTE:** I'm looking Amiga and MSDOS terminal supporting color and control codes of linux, so it will be possible to use Midnight Commander in terminal connection. If you know such terminal application, then let me know.

## PPP connection in Windows 95 on ao486
Unfortunately winsock and winsock2 provided by Microsoft do not work with the ppp connection when in Windows 95.

The following steps will allow you to get it working.

1. In the Mister System Menu ( Win/F12 ) set the "Uart Connection" to "PPP" and save it.
2. In Windows 95 ensure the COM1 device is installed in Start->Settings->Control Panel->System - Device Manager Tab, there should be a twisty called Ports(COM & LPT) and under that a "Communications Port (COM1)"
3. If it doesn't exist go to Start->Settings->Control Panel->Add/New Hardware and it should be automatically added.
4. Get the replacement PPP client
    * Download the software.  There are other newer versions available BUT be warned only version 3.0 will work.
        * [Trumpet Winsock 3.0](https://winworldpc.com/product/trumpet-winsock/3x){target=_blank} - (I extracted the file from the disk image and uploaded it using the DOS ftp client documented above)
5. License the Software - This software is still shareware (time limited) please license it appropriately. Once you acquire a license you can put the details in Tcpman in the "Special" menu in "Password registration"
6. Configure Software  
    * Start Tcpman
    * Under File-->PPP Options ensure all checkboxes are unchecked and the text boxes are blank.
    * Under File-->Setup Enter an "IP Address" suitable for your LAN eg 192.168.1.254 and a "DNS Server(s)" 192.168.1.1
        * Under the Driver section select the PPP radio button and click on "Dialer settings..."  
    * In the "Dialer settings..."  
        * "COMM port" COM1  
        * "Baud rate" 115200
7. Using the software ( important, be patient )
    * Win95 is rather slow so let it start fully before starting the PPP manager (Tcpman)
    * Once it is started it will begin syncing with PPP on the linux host... Be patient it takes a few seconds.
    * When you see the PPP[C021] SND and RCV you can start your TCP/IP program

I have found it to be a little complicated to get started, but once it is running it is rock solid and supports multiple client programs at once.

## Serial connection on C64
The following is an example for connecting to a BBS using Striketerm 2014.

1. Start the C64 core (please note that custom kernels may remove functionality required, if in doubt use the built in kernel).
2. In the Mister C64 Menu ( Win/F12 ) set the "User Port" to "UART", and save it.
3. In the Mister System Menu ( Win/F12 ) set the "Uart Connection" to "Midi", "Remote", "TCP" and save it.
4. Load Striketerm 2014 from d64. Available from [here](https://csdb.dk/release/?id=130807){target=_blank}
5. Keep the defaults in the Main Menu (F1), ensure you are running at 2400 baud.
6. Save a BBS into the Addressbook (F5), you can get some from [here](http://cbbsoutpost.servebbs.com){target=_blank}
7. Surf the BBS very slowly...
