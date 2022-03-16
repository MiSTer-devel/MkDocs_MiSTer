---
hide:
  - toc
---

This page explains most of the intricacies of the way MiSTer handles ROMs for Arcade systems.

## MRA Format

Because some arcade boards can change games by just putting in new roms, it made sense to move the RBF files out of sight from the menu list, and browse the MRA files instead. These MRA files specify which RBF file to use, and which mame rom zip files to create on the fly into a rom to pass to the arcade core. They will create the old a.pacman.rom style rom on the fly from mame roms, either merged or non-merged.

### Here is an example of where the files might go:
```bash
/_Arcade/<game name>.mra
/_Arcade/cores/<game rbf>.rbf
/_Arcade/mame/<mame rom>.zip
/_Arcade/hbmame/<hbmame rom>.zip
```
There are other locations for these files based on search paths.

### MRA Format
```xml
<misterromdescription>
  <name>Donkey Kong (US set 1)</name>
  <mratimestamp>201911270000</mratimestamp>
  <mameversion>0216</mameversion>
  <setname>dkong</setname>
  <year>1981</year>
  <manufacturer>Nintendo of America</manufacturer>
  <category>Maze / Monkeys</category>
  <category>Platform</category>
  <category>Platform / Mario Bros.</category>
  <rbf>DonkeyKong</rbf>
<!-- switches element taken from "Pac-Man (Midway).mra"; for demonstration purposes only -->
  <switches default="FF,FF,C9">
    <dip bits="15"    name="Cabinet" ids="Cocktail,Upright"/>
    <dip bits="16,17" name="Coinage" ids="2c/1cr,1c/1cr,1c/2cr,Free Play" values="3,1,2,0"/>
    <dip bits="18,19" name="Lives" ids="1,2,3,5"/>
    <dip bits="20,21" name="Bonus Life After" ids="10000,15000,20000,None"/>
    <dip bits="22"    name="Difficulty" ids="Hard,Normal"/>
  </switches>
  <buttons names="Jump,Start 1P,Start 2P,Coin" default="A,Start,Select,R"/>
<!-- rom index 1 or any other index can pass additional information to a rom.
useful to say this rom is game A or game 1.  Use it in case of multiple games for
the same RBF, ie: Dig Dug 2, Mappy -->
  <rom index="1">
    <part>0A</part>
  </rom>
<!-- romstruct element taken from "Two Tigers.mra"; for demonstration purposes only -->
  <romstruct>
ROM structure
00000 - 0BFFF  48k CPU1
0C000 - 0FFFF  16k CPU2
10000 - 13FFF  16k GFX1
14000 - 1BFFF  32k GFX2
  </romstruct>

<!-- the nvram node is used to download and upload the nvram memory. When the user hits "Save Settings" in the OSD it triggers ioctl_upload. This isn't available in Donkey Kong because it didn't originally have NVRAM -->
<nvram index="4" size="1024"/>



<!-- rom index 0 is the standard rom. The zip will be added to the name inside the part, unless the
part has it's own zip. The md5 will be checked at the end. A file not found error is reported before an md5
error. -->
  <rom index="0" zip="dkong.zip" md5="05fb1dd1ce6a786c538275d5776b1db1" type="merged|nonmerged|split">
    <part crc="ba70b88b" name="c_5et_g.bin"/>
<!-- interleave element taken from "Crater Raider.mra"; for demonstration purposes only -->
    <interleave output="32">
	<part crc="579a8e36" name="crvid.a4"  map="0001"/>
	<part crc="2c2f5b29" name="crvid.a3"  map="0001"/>
	<part crc="5bf954e0" name="crvid.a6"  map="0010"/>
	<part crc="9bdec312" name="crvid.a5"  map="0010"/>
	<part crc="4b913498" name="crvid.a8"  map="0100"/>
	<part crc="9fa307d5" name="crvid.a7"  map="0100"/>
	<part crc="7a22d6bc" name="crvid.a10" map="1000"/>
        <part crc="811f152d" name="crvid.a9"  map="1000"/>
    </interleave>
<!-- begin kill screen fix -->
    <patch offset="0xf7d">
FE 04 38 02 3E 04 47 A7 17 A7 17 A7 17 80 80 C6 
28
    </patch>
<!-- end kill screen fix -->
    <part crc="d6412358" name="c-2j.bpr"/>
    <part crc="b869b8f5" zip="another.zip" name="v-5e.bpr"/>
    <part crc="b869b8f5" name="v-5e.bpr" offset="1024" length="1024"/>
    <part repeat="3328">00</part>
    <part>
80 80 80 80 80 80 7F 7F 7F 7F 7F 7F 7F 80 80 80
    </part>
  </rom>
<!-- If the first rom0 fails the md5 checksum, it will go ahead and try again if another entry is present.
Otherwise it will skip the additional entries.
-->
  <rom index="0" zip="dkong.zip" md5="05fb1dd1ce6a786c538275d5776b1db1">
  </rom>
</misterromdescription>

```

When creating a core you can pass additional data in using ioctl_index > 0. 

```verilog
// Retrieve Title No.
always @(posedge clk_sys) begin
   if (ioctl_wr & (ioctl_index==1)) tno <= ioctl_dout[3:0];
end

```

### Explanation for XML elements and attributes
* **name**: As an element this indicates how the rom should be called. The value should be taken from MAME. As an attribute this indicates an external rom file (or part thereof) that should be loaded by MiSTer.
* **mratimestamp**: This indicates the date on which the *.mra file was created (useful for other users to determine if there is a newer version of the *.mra file available to which they should upgrade). The date format is yyyymmdd.
* **mameversion**: This indicates on which version of a MAME romset the *.mra file is based (which version was used for testing). The dot in MAME's version numbering is omitted.
* **setname**: This indicates the name of the romset used as given by MAME. It is used to overwrite the core ID specified in the *.rbf file so that individual settings can be saved on a per romset basis.
* **year**: This indicates the year the game was released. The format is YYYY and the value should be taken from MAME.
* **manufacturer**: This indicates the manufacturer of the game. The value should be taken from MAME.
* **rbf**: This indicates the filename (sans path and extension) of the core that should be used to run the game.
* **buttons**: This indicates the default button mapping for the game. As the name implies, it only implies to buttons, not to directional controls. The **names** attribute specifies how the buttons are called in the MiSTer OSD while the **default** attribute specifies how the buttons are mapped to the virtual [MiSTer gamepad](../setup/controller.md).
* **switches**: This is to define the dip switches present on the arcade board. As this is a bit more complex, there is a [specific section](#Dip-Switches) for it below.
* **nvram**: This tells MiSTer to save the NVRAM data on Save Settings in the OSD. If an NVRAM was saved, it will be sent to the core as well
* **romstruct**: This is to give information about the rom structure, how the rom memory is mapped. Information contained herein is intended as a comment for other developers and not actually used by MiSTer.
* **remark**: This element is intended for general remarks. Information contained herein is intended as a comment for other developers and not actually used by MiSTer.
* **rom**: Part, patch and interleave elements must have a rom element as a parent element. An **index** attribute with a value of 1 is used to pass information to multigame cores, which machine configuration to use. For passing actual rom data you need an index value of 0. The **md5** attribute is used to specify the md5 checksum. The md5 checksum is calculated and checked by MiSTer after the whole rom is created according to the given *.mra file. You can use the Linux console to find out the checksum calculated by MiSTer when it starts the core (the command line to do so is '/media/fat/MiSTer rbffilename mrafilename'). Roms whose checksum differ from the one specified in the *.mra file won't load. Specifying the md5 checksum as “none” will disable this check.
* **part**: The part element is only allowed inside a rom element. It is used for specifying a part of the rom. The content of a part can either be embedded as a hex value into the *.mra file itself (if copyright law allows) or there can be a reference to an external file via the name attribute. If the external file is in a different zip file than the parent rom element, the filename of the zip file must be specified via the **zip** attribute.
  * The **crc** attribute specifies the CRC32 checksum of the respective part (format: eight hex digits). If a crc value is specified, MiSTer will try to select the appropriate file by crc (and only revert to the filename specified by the attribute name, if the crc value does not match). This increases compatibility of the *.mra file with different MAME versions of the romset. As crc values are only relevant for external files, a crc value should only be given to a part element when there is a reference to an external file.
  * The **repeat** attribute only applies to embedded parts and indicates for how long (not how many times) the sequence should be repeated. By default decimal numbers are assumed. Hex numbers must be preceded with "0x".
  * Inside the rom element, the **offset** and **length** attributes only apply to external files. To use the offset attribute for internal data, the patch element must be used. Offset indicates the location inside the file from where MiSTer should start reading and length indicates the length of the sequence that MiSTer should be reading. By default decimal numbers are assumed. Hex numbers must be preceded with "0x".
  * The **map** attribute specifies to only read certain parts of the corresponding part element. For example a value of "0001" (binary) means to read only every fourth byte while a value of "1010" (binary) means to read only every first and third byte. To byteswap a part you need to set a map attribute value of 21 (decimal) and enclose the respective part element in an interleave tag.
* **patch**: The patch element is only allowed inside a rom element. It is applied after the whole rom is created from its parts and overwrites the content of the rom with the content of the patch element, starting from the specified offset and for the length of the patch element's content.
* **interleave**: The interleave element is only allowed inside a rom element and can only be used as parent element to one or more part elements. Together with the mandatory **output** attribute the interleave element can be used to specify that the children part elements should be read in a certain way. For example an output-value of "32" (decimal) indicates that the children part elements ROM data should be treated as 32 bit.

### Dip Switches

Dip switch support in the latest version of MRA is used instead of the status bits. The DIP config str is listed in the core, and the core is responsible for reading the up to 64bits of dip data that is sent via ioctl_index 254.


```verilog
reg [7:0] sw[8];
always @(posedge clk_sys) if (ioctl_wr && (ioctl_index==254) && !ioctl_addr[24:3]) sw[ioctl_addr[2:0]] <= ioctl_dout;
```

Switches is the dip switch setting. The **default** are the default bytes. These are used so you can default the arcade into the proper factory settings. This is useful when the factory settings aren't all OFF/OFF/OFF. Note that in the **default** hexadecimal string, the leftmost byte refers to DIP bits 7:0, the next byte to 15:8 and so on. The most significant byte thus occupies the rightmost part of the string.

```xml
 <switches default="FF,FF,C9">
```

The value C9 will apply to DIP bits 23:16.

The dip tag let's you put in a dip switch entry. The bit number (starting at 0) is based on the way the core was written. Often MAME source code can be used to understand the bits. The numbering will depend on the rom used, the arcade core, and how things are laid out.
 
* **bits**: bit number to fill out sent to the core in ioctl_data
* **name**: title for the OSD
* **ids**: title for each option in the OSD
* **values**: if you want the values to be different than 0,1,2,3 you can reorder them
 
```xml
    <dip bits="16,17" name="Coinage" ids="2c/1cr,1c/1cr,1c/2cr,Free Play" values="3,1,2,0"/>
```
