# MERA ELZAB ComPAN 8/16-bit MICROCOMPUTER

## SYSTEM OVERVIEW

ComPAN 8 is an 8-bit Polish microcomputer produced in the 1980s at the MERA-ELZAB factory in Zabrze, Poland. 
ComPAN 8 was designed at the Institute of Industry Automation Systems PAN in Gliwice.
My unit is from 1988 and has a S/N of 396 and it labelled as 'Microcomputer 8/16-bit'. 
The exact number of manufactured units is unknown but is estimated at ~100 units a year.
The number of survived units is unknown, but I'd say a few. 
The '8/16-bit' most likely due to a fact that it has a 8088 card (probably a compatibility card for DOS software).
Comes with two RAM boards of 896K of 'common RAM'. Advertisements I found claims it could a RAM disk.
It has extended address bus (A0 - A19), so it can address up to 2Mb instead of 64k that 8080 can.

## SCHEMATICS

All the schematics here are reverse engineered by me (only the CRT part are somewhat original, since they are from a MERA 7953N terminal).

****THEY MIGHT CONTAIN ERRORS****

## EPROM/PROM DUMPS

Eproms and Proms are dumped by me on TL866II.
There should not be any issues with eprom dumps, but PROMs are dumped like 27xx series EPROM and saved in HEX format. 
Since the difference in the size of PROM and 2716 I used as a reader preset so the content is looped.

## VIDEO SUBSYSTEM
ComPAN comes in a form we would call 'AIO' today. The screen is monochrome, known are units with green and amber CRTs. It is said that amber CRTs were B/W with amber coating that is not a phosphor. 
The video parameters are of composite video  - HSync of 15 kHz, VSync of 50 Hz.
The video board has no dedicated video controller but is based on three 8255s. It has 64k x 12 bit(!) of screen memory (on VIDEORAM 2 board). 
It suports underline, inverted, blinking and different chargen modes.
Bottom 4 rows of 80 characters each is a system window, the upper part of the screen contains:
- 24 rows of 80 chars in char only mode,
- 30 rows of 80 chars in char-graphics mode,
- 640 x 288 dots in graphics mode.

## KEYBOARD
It uses a MERA 7946M-like keyboard. The KB interface consists of 8 data lines and STROBE signal. Keyboard is handled by 8255 on VIDEORAM1 board.
There was also a dedicated keyboard, based on i8035.
The keyboard looks like one for MERA 79152 PC but without the status LEDs.
The dedicated keyboard also uses two more signals. /INT and T0 for the 8085.
The keyboard matrix is based on RTF hall efect switches, with enable input, - VEB HFO B 461 G.
More on the hall switches from RFT: https://telcontar.net/KBK/HFO/Hall_ICs


## STORAGE  
ComPAN has Rockwell 6765 FDC and can use up to 4 5,25 inch FDDs.
There are modules with two FDDs or one FDD and 20Mb Winchester.
The Winchester controller is inside the drive module and seems to use a FDD interface to connect to system.


![alt text](https://github.com/RetroNora/Elzab_ComPan_8/blob/main/ComPAN.jpg)


