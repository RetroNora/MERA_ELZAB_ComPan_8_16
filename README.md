# MERA ELZAB ComPAN 8/16-bit MICROCOMPUTER

## SYSTEM OVERVIEW

ComPAN 8 is an 8-bit Polish microcomputer produced in the 1980s at the MERA-ELZAB factory in Zabrze, Poland. 
ComPAN 8 was designed at the Institute of Industry Automation Systems PAN in Gliwice.
My unit is from 1988 and has a S/N of 396 and it labelled as 'Microcomputer 8/16-bit'. 
The exact number of manufactured units is unknown but is estimated at ~100 units a year.
The number of survived units is unknown, I know about ~15 units. 
The '8/16-bit' comes from i8088 card that shares system resources with i8080.

<p align="center">
<img src="https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN_plate.jpg" />
</p>


That means I have a dual CPU unit that should be able to run different OSes. 

<p align="center">
<img src="https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN%20graph.png" />
</p>

Comes with two RAM boards of 896K of 'common RAM'. Advertisements I found claims it could use a RAM disk.
It has extended address bus (A0 - A20), so it can address up to 2Mb instead of 64k that i8080 can address.

The extension of address bus is achieved on 8080 board (in fact they are outputs of 8212s). Additional address bits are handled by PROMs (on boards that they need it).

<p align="center">
<img src="https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN%20block.png" />
</p>



![alt text](https://github.com/RetroNora/Elzab_ComPan_8/blob/main/ComPAN.jpg)

## P1/P2 CONNECTORS
Each card comes with two 92 contact card edge connectors. P1 at the top of the board and P2 at the bottom. P1 is a system bus connector (address + data + IRQs + control signals). It has the same pinout on every board. 
P2 is dedicated to each board role, and the pinout differs board to board. The boards are connected with backplane. Each slot is dedicated to specyfic card type, connecotrs are keyed. The keying is done with missing ground pins and plastic tabs in slots.

The layout is:

[         CRT MODULE        ]

[1][2][3][4] PSU [5][6][7][8]

1 - VIDEORAM 1,

2 - VIDEORAM 2,

3 - 8088 BOARD,

4 - EMPTY,

5 - I/O BOARD,

6 - RAM,

7 - RAM,

8 - 8080 BOARD.

The press releases about ComPAN show different layout, I think it's due to ComPAN 8 and ComPAN 8/16 differences.

## SCHEMATICS

All the schematics here are reverse engineered by me (only the CRT part are somewhat original, since they are from a MERA 7953N terminal).

****THEY MIGHT CONTAIN ERRORS****

## EPROM/PROM DUMPS

Eproms and Proms are dumped by me on TL866II.
There should not be any issues with eprom dumps, but PROMs are dumped like 27xx series EPROM and saved in HEX format. 
***NOTE THE DUMPS ARE 8-BIT BUT PROMS ARE 4-BIT***

## I/O CONNECTORS

![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN_IO.jpg)

## 8-bit CPU (i8080) BOARD
This board comes with i8080 CPU, i8224 clock generator, i8228 system controller and system ROM. This board also has 2k of SRAM used to test the system on boot even if RAM on RAM Board has failed (Common RAM error).
The DMA handling and expansion of address bus (16 --> 21) happens to this board. i8257 DMA controller and 7 i8212 are responsible for it. Each DMA channel got it's own 8-bit I/O port (8212), 8257 supplies the system with 4 DMA channels. The i8080 board is equiped with i8259 IRQ controller, the system has 8 IRQs. 
This board comes with two i8253 programable timers.
Also two RS232C serial ports are handled by CPU board.

![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/8080%20CPU.jpg)

Address decoding/ select logic is made on 5 82S129 (256x4 PROM) and one 74138.

<p align="center">
<img src="https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/PROM_DUMPS/PROCESOR_8080/8080_PROM.jpg" />
</p>



## VIDEO SUBSYSTEM
ComPAN comes in a MERA 79xx series terminal case (slightly bigger than standard terminal). The screen is monochrome, known are units with green and amber CRTs. It is said that amber CRTs were B/W with amber coating outside the tube (not phosphor). 
The video parameters are of composite video - HSync of 15,625 kHz, VSync of 50 Hz.
The video board has no dedicated video controller but is based on three 8255s. It has 64k x 12 bit(!) of screen memory (on VIDEORAM 2 board). 
It suports underline, inverted, blinking and different chargen modes.
Bottom 4 rows of 80 characters each is a system window, the upper part of the screen contains:
- 24 rows of 80 chars in char only mode,
- 30 rows of 80 chars in char-graphics mode,
- 640 x 288 dots in graphics mode.

## VIDEORAM1 BOARD
  VIDEORAM1 is responsible for generating the video signal, sync signals, keyboard input and interfacing to screen memory.
  Three golden K573RF2 EPROMS at the bottom contain ASCII/ semigraphics and alt graphics.
  
  The contents of these RF2s:

GZASCII

  ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Fonts/GZASCII.jpg)

GZSEMI

  ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Fonts/GZSEMI.jpg)

GZALT

  ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Fonts/GZALT.jpg)

  (I got these set of fonts thanks to help of [technomancer-lv ](https://github.com/technomancer-lv).)

  
  
  ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/VIDEORAM1.jpg)

  
## VIDEORAM2 BOARD
  VIDEORAM2 is a screen memory of 64k of 12-bit words. It uses KR565RU6 that are soviet 4116s with just single VCC of +5V. 
  CPU also can have a direct connection to VRAM.
  It also comes with three 2114 (here TMM314AP) so 1024x12 SRAM.
  
  ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/VIDEORAM2.jpg)

  
##  8088/8087 board
This is a special board that makes my ComPAN 8/16bit microcomputer. This card places my unit somewhere in between ComPAN - 8 and ComPAN-16 that never entered mass production. 
The unit is from 1988 but I found mentions about i8088 card from as early as 1986.
The BIOS for ComPan i8088 card was made by ZSAK PAN Software Corporation and has a compilation date of 11/08/82.
I don't know how many of ComPANs that survived to today are 8/16 model.
The BIOS also mentions colour graphic/ XT keyboard and seems to have HDD handling procedures. 


 ![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/8088%20board.jpg)
 
## KEYBOARD
It uses a MERA 7946M-like keyboard or a dedicated keyboard based on MERA 79152PC keyboard. 

![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN_keyboard.png)

The parallel keyboard interface consists of 8 data lines and STROBE signal. Keyboard is handled by i8255 on VIDEORAM1 board.
The dedicated keyboard is based on i8035.
The dedicated keyboard also uses two more signals. /INT and T0 for the i8085.
The keyboard matrix is based on RTF hall efect switches, with enable input, - VEB HFO B 461 G.
More on the hall switches from RFT: https://telcontar.net/KBK/HFO/Hall_ICs

Commercials and BIOS strings mention PC-XT style keyboard option. 

![alt text](https://github.com/RetroNora/Elzab_ComPan_8/blob/main/keyb.jpg)

## MEMORY
ComPAN has a feature of expanded address bus to 21 lines (A0 - A20), and can address up to 2 MB of RAM. Since 8080 address space ends on 64k it has to use RAM banking.
The computer has a i8257 for handling the DMA transfers.
Mine unit got two 128/512k RAM boards. One got full 512k, the other 384k. 
It seems that the board could be populated with 4116 (128k) or 4164 (512k).
It has jumpers that need to be set according to ICs used.


![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/RAM%20map.png)



## STORAGE  
My ComPAN has Rockwell 6765 FDC and can use up to 4 5,25  or 8 inch FDDs.
The FDC is located on I/O board with the FDD connectors on the back of the unit. 
It seems to use standard Shugatr interface, for FDD there is no logic inside the drive module, just a cable pass thru. 
There are modules with two FDDs or one FDD and 21Mb Winchester.
The Winchester controller(WD1010) is inside the drive module and seems to use a FDD interface to connect to system.

## SOFTWARE
By MFM Archiver/ Emulator from pdp8online (https://www.pdp8online.com/mfm/mfm.shtml) I was able to copy contents of one of my 21Mb drives (the second had a head crash, probably while still operating in the first owner).
I was able to recover a system partition of 

**The ComPAN-16 Personal Computer DOS (IBM compatible)**

**Version 3.10 Implemented by ZSAK-PAN 1985, 1986, 1987**

Sadly the drive had no computer-specific software, just a copy of Norton Commander and a polish-made antivirus software.
Recovering a boot floppy image is just a matter of time.

 
## STATE OF MY UNIT

It seems that on 384k RAM board there is an issue. Without this board the computer is able to make it to boot screen.

![alt text](https://github.com/RetroNora/MERA_ELZAB_ComPan_8_16/blob/main/Pics/ComPAN_boot.jpg)

Sadly, any keyboard input freezes the machine or makes it's screen roll.







