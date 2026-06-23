# SB-mini-II
A homebrewed Apple II clone

## Hardware Overview

- The CPU is a standard 65C02 running at near 1.024 MHz (the original Apple II ran at 1.023 for the 60 Hz models), after dividing the 4.096 MHz crystal by 4.
- The 12kB ROM image is placed on the 32k EEPROM. Becuase there's spare room on this chip a jumper allows for selecting the high or low half of the ROM chip, so I've placed Ardian Black's Deadtest program in there.
- 48kB of RAM is accomplised by using one and half 32kB SRAM chips. Figured this was easier to use matching chipd than it was to use a 32kb + 16kB chip.
- Address decoding works exactly like the real Apple II. This was mostly based on the schematics in _Understanding The Apple II_ by Jim Sather.
- In Addition to the I/O slots, this has:
  - Speaker: matching the genuine Apple II
  - Game I/O: as the NE558 quad timer is hard to find, I've [implemented this replacement using a pair of 556 chips](https://github.com/roybaer/ne558_replacement).
  - Keyboard: a Raspberry Pi Pico provides a modern USB interface but electrically it connects to the Apple II in the same way as the original ASCII keyboard did. The Pi can also generate a reset pulse when pressing Control + Print Screen, and also performs a power-on reset for the system. The firmware for this is [in this project here](https://github.com/simonboak/SB-mini-II-Keyboard).
  - Graphics: there is absolutely no onboard hardware for displaying graphics. Instead you'll want to use an [Apple VGA Card](https://github.com/markadev/AppleII-VGA).
- Features deliberately missing:
  - Expansion slots do not provide the DMA, USER 1 or 7M clock signals.
  - The bus is not buffered: with a CMOS design this is less likely to be a problem (although no guarantees for interfacing with cards using 74LS logic).
  - There is no cassette input or output.
- These are the Revision 1 files. Rev 0 was a smaller board with no 5V regulation, only 7 slots and 32k on board RAM. The plan had been to leave out slot 0 and work out how to make full use of a second 32k RAM chip to have the full 64k without needing a language card, however this almost doubled the amount of circuitry needed.

## 3D Printed Case

Combining the design of the Apple II with the ProFile hard disk, the case requires a bit of assembly:

1. Print each piece with the flat side on the print bad (you could print the lid pieces as one if desired)
2. Glue the "tongue" into the slot along the bottom inside edge of the front piece. This will locate into the notch inside the front of the base.
3. Glue the top, front and sides together.
4. For the light pipe it was filled with hot glue to create a diffused lense with the LED glued in behind.
5. The base requires 8x M3 threaded inserts, 2 of which are for the back panel, the rest are the PCB mounts.
6. The 20mm speaker can be taped into the round hole in the base.