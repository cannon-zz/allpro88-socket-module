# KiCad Model of Logical Devices' ALLPRO88 PLCC Socket Module

## Overview

This provides a KiCad [schematic](https://github.com/user-attachments/files/20514003/socket_module_plcc_schematic.pdf) of the PLCC socket module for use with Logic Devices' ALLPRO88 software-driven device programmer.  The service manual scans available on the internet are incomprehensible.  I believe the schematic is correct.  The PCB's size and the locations of the DIN connectors, 48 pin ZIF connector and decoupling capacitors and transistors all match the original.  All other part locations are approximate, the PCB has not been routed, and the footprints for the PLCC sockets are not correct.  The PLCC sockets here have the wrong pin layout, and are mirrored with respect to the originals (the originals are "dead bug" style sockets, into which the parts get inserted upside down).  The objective is not to allow a PLCC socket module to be reproduced from this project, but to provide a starting point for making a custom socket module.

## Board Size

Measuring my PCB to the nearest 0.5 mm, the PCB is 25.70 cm x 20.45 cm.

If it's imperial, and we allow some +/- for the saw cut accuracy, it could be 10 1/8" x 8" (= 25.7175 cm x 20.32 cm).

I found a comment in the service manual that the PCB is 10.100" x 8.05x" (x is unreadable, could be 0, 6 or 8 maybe).  0.001" = 0.0254 mm, so I don't think it really matters if that digit is a 0 or an 8.  10.1" x 8.05" = 25.65 cm x 20.45 cm which is within 0.5 mm of my measurements.

## DIN Connector Placement

I suggest plugging the DIN connectors into the base, then placing the PCB onto them and either tightening the screws to hold them in that position or soldering enough pins to secure them, then removing the PCB with the connectors to continue soldering.  That way they're guaranteed to be aligned with their sockets after being soldered into position.
