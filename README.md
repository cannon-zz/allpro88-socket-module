# KiCad Model of Logical Devices' ALLPRO88 PLCC Socket Module

## Overview

This provides a KiCad [schematic](https://github.com/user-attachments/files/20514003/socket_module_plcc_schematic.pdf) of the PLCC socket module for use with Logic Devices' ALLPRO88 software-driven device programmer.  The service manual scans available on the internet are incomprehensible.  I believe the schematic is correct.  The PCB's size and the locations of the DIN connectors, 48 pin ZIF connector and decoupling capacitors and transistors all match the original.  All other part locations are approximate, the PCB has not been routed, and the footprints for the PLCC sockets are not correct.  The PLCC sockets here have the wrong pin layout, and are mirrored with respect to the originals (the originals are "dead bug" style sockets, into which the parts get inserted upside down).  The objective is not to allow a PLCC socket module to be reproduced from this project, but to provide a starting point for making a custom socket module.

## Board Size

Measuring my PCB to the nearest 0.5 mm, the PCB is 25.70 cm x 20.45 cm.

If it's imperial, and we allow some +/- for the saw cut accuracy, it could be 10 1/8" x 8" (= 25.7175 cm x 20.32 cm).

I found a comment in the service manual that the PCB is 10.100" x 8.05x" (x is unreadable, could be 0, 6 or 8 maybe).  0.001" = 0.0254 mm, so I don't think it really matters if that digit is a 0 or an 8.  10.1" x 8.05" = 25.65 cm x 20.45 cm which is within 0.5 mm of my measurements.

## DIN Connector Placement

I suggest plugging the DIN connectors into the base, then placing the PCB onto them and either tightening the screws to hold them in that position or soldering enough pins to secure them, then removing the PCB with the connectors to continue soldering.  That way they're guaranteed to be aligned with their sockets after being soldered into position.

## Signal Names

The scans available on the internet of the original schematic, both for the socket module and the programmer's mother board, are incomprehensible.  Also, there are several inconsistent channel numbering schemes in Logical Devices' original documentation.  So:  what's here is my own invention.  Make of it what you will.

 * GND:  system power supply return.
 * -8 V, -5 V, +5 V, +12V, VREF:  main system power supplies.
 * VADJ:  main programmable, high current, power supply.  All pin driver voltages are derived from this.
 * VSR, VTH, VPU, ILIN:  pin driver power supplies.
 * !SOCKETEN:  active-low device select line indicating that the address bus is in the range 0x0280 to 0x02ff inclusively.  This is a 128 byte window reserved for the socket module.  On the universal PLCC module, reading from any address in this range returns the socket module ID, while writing to addresses in this range control the registers used to switch the pin decoupling capacitors on and off.
 * \phi_{0}, \phi_{1}:  the two phases used for driving the TTL clock output modes of the pin drivers.  When they are active they are guaranteed to be 180 degrees out of phase, but they can become inactive and enter the same state.
 * !XFER:  active low line to clock the pin driver DACs
 * !RD, !WR:  active low read- and write-enable signals.
 * !LED_BUSY, LED_IDLE:  common collector drives for the busy (red) and idle (green) LEDs.
 * !RESET:  active low system reset.  On the PLCC module, resets the decoupling capacitor registers to 0 (capacitors disconnected).
 * !SELECT0 -- !SELECT4:  active low device select lines for the first 5 pin driver modules, corresponding to channels 0 through 39 inclusively.  The ALLPRO88 was preceded by an earlier product that had only 40 channels, and it was presumably thought to be handy to have these signals brought out to the socket module to avoid duplicating address decoding circuitry in the event that lots of complex pin driver circuitry was needed for some part.
 * A0 -- A9:  partial system address bus.  The system address bus is 12 bits, but only the low 10 are present on the socket module.  Together with !SOCKETEN, only A0--A6 are needed to address the 128 byte window reserved for the socket module.
 * D0 -- D7:  system data bus.
 * OUT0 -- OUT87:  the 88 pin driver inputs/outputs.
 * SPARE1:  unused signal line that connects to the socket module, all pin driver boards, and both analogue 1 and analogue 2.  There are two unused voltage DACs on analogue 2, and I think a sensible thing to do would be to jumper one of them to this in line, to provide an additional programmable voltage to the system.  For example, the fixed 5 V linear regulators that generate the "TTL" output voltage on the pin driver boards could be replaced with adjustable regulators programmed by this voltage, making it easier to support non- 5 V logic.
