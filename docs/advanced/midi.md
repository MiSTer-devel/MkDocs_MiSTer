When running the Minimig and ao486 cores, once a ALSA compatible USB MIDI device is attached, two additional ‘UART Connection’ menu options (‘USBMIDI’ and ‘USBMIDI-38K’) will be available in addition to ‘None’, ‘PPP’ and ‘Console’.

## Minimig

‘USBMIDI’ - This option is used with the Amiga / Minimig core. This option sets the UART connection speed to 31250 baud which is the standard MIDI speed.

Many Amiga applications and most games don’t require any additional drivers for MIDI. Some “newer” applications may require the CAMD driver.

[Aminet : CAMD](http://aminet.net/package/mus/midi/camd){target=_blank}

## ao486

‘USBMIDI-38K’ - This option is used with the ao486 core. This option sets the UART Connection speed to 38400 baud. (The MIDI speed of 31250 baud is not a standard speed DOS PC UARTs were capable of doing)

While some sequencer applications and Microsoft Windows may support MIDI on the serial port, DOS games typically require a MPU-401 interface which ao486 unfortunately lacks. In lieu of hardware MPU-401 capability the SoftMPU TSR can be used with a good degree of success.

[SoftMPU](http://bjt42.github.io/softmpu/){target=_blank}

## SoftMPU

SoftMPU requires the QEMM memory manager be installed. For testing QEMM 8.03 was used. QEMM “stealth” option seems to be incompatible with ao486 so it is advisable to skip that part of the optimize process. It’s a good idea to run the QEMM optimize application again after installing SoftMPU (in the AUTOEXEC.BAT) to get as much of the lower 640K conventional RAM free as possible.

Although less common, some DOS games and applications require MPU-401 interrupts. This option can break compatibility with others software not requiring interrupts.


Starting SoftMPU without MPU-401 interrupts:

    SOFTMPU.EXE /MPU:330 /OUTPUT:COM1

Starting SoftMPU with MPU-401 interrupts:
       
    SOFTMPU.EXE /SB:220 /IRQ:5 /MPU:330 /OUTPUT:COM1  

The Rev.0 Roland MT-32 used in testing required the ‘DELAYSYSEX’ switch to prevent buffer overflow for certain games but made Sierra games upload sysex commands excessively slowly. This is not necessary for General MIDI modules and newer revision MT-32s.

    SOFTMPU.EXE /MPU:330 /DELAYSYSEX /OUTPUT:COM1

## MidilLink

The 'midilink' daemon currently supports following switches / options:

```
TESTSER  - this option sends a test message to the serial port once 
           the daemon is started.  

TESTMIDI - this option sends a middle 'c' note to the MIDI device 
           once the daemon is started. 

QUIET    - this option suppresses MIDI debug output.  

38400    - this option sets the serial speed to 38400 baud 
           (default is 31250 baud) - used with ao486 core.
```

[MidiLink Github](https://github.com/bbond007/MiSTer_MidiLink){target=_blank}

## MIDI Adapters reported to work

* Creative EMU XMIDI (Known to mangle SYSEX messages)
* Roland UM-ONE
* M-Audio Midisport Uno

## MT32-pi Video Example
![type:video](videos/mt32-pi.mp4)
