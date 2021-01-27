# Fanashifter

Project about how to connect shifters (sequential or H-shaped) on Fanatec Wheel bases, using it's internal
protocol. Tested with a sequential shifter on CSL elite 1.1. Also the 3D models for the Levers and electronics are provided.
In this example, we can connect directly our shifter levers to port Shifter2 (rj12) also works on Shifter1.

# Table Of Contents

1. [Project Features](#project-features)
2. [3D Printing and Assembly](#3d-printing-and-assembly)
    1. [Prototype](#prototype)
    2. [CatFeeder](#catfeeder)
        1. [Part list to print](#part-list-to-print)
        2. [Printing times](#printing-times)
        3. [Assembly](#assembly)
            1. [Mount the pins in the inner case](#mount-the-pins-in-the-inner-case)
            2. [Screw the base to the inner case](#screw-the-base-to-the-inner-case)
            3. [Mount the axis motor and support](#mount-the-axis-motor-and-support)
            4. [Iron the wires to battery holder](#iron-the-wires-to-battery-holder)
            5. [Build the 90 degree wires](#build-the-90-degree-wires)
            6. [Wiring diagram](#wiring-diagram)
            7. [Mount the UNL2003](#mount-the-unl2003)
            8. [Mount the ESP8266](#mount-the-esp8266)
            9. [Mount the cap](#mount-the-cap)

3. [How to install the Software](#how-to-install-the-software)
    1. [Arduino Board Setup](#arduino-board-setup)
    2. [Configuration options](#configuration-options)
    3. [Download the components to the Board](#download-the-components-to-the-board)
        1. [Check for good compilation](#check-for-good-compilation)
        2. [Download the FileSystem to the board](#download-the-filesystem-to-the-board)
        3. [Download the CatFeeder application to the board](#download-the-catfeeder-application-to-the-board)
4. [Configure CatFeeder](#configure-catfeeder)
    1. [Connect to the AP](#connect-to-the-ap)
5. [Using Catfeeder](#using-catfeeder) 
    1. [Calibration](#calibration)
    2. [Configure Schedules](#configure-schedules)

## Project Features

1. Fully printable, so you can download the project, start your printer, and print all the parts. The STL are 
ready to print, so the orientation and tolerances are configured and tested.
2. Uses the standard RJ12 port with it's internal protocol, so just plug and play.
3. Cheap to build. Based on standard hardware components:
    * Printed on PETG
    * Some wiring cable (8 wires)
    * 30 allen screws (13mm)
    * 4 allen screws (6mm)
    * 2 standard micro switch NO 
    * a RJ12 to RJ12-6p6c (all poles connected, 1-1) cable, to do the wiring.
    * 2 springs

## Pinout RJ12 (6P6C)

<img src="images/pins.jpg" width="200"/> 

Documentation from:

https://hackaday.io/project/171155-fanatec-clubsport-shifter-sq-v15-usb-adapter-diy

https://www.gtplanet.net/forum/threads/conversion-of-a-logitech-shifter-for-fanatec-wheelbase-compatibility-enabling-7th-gear-other-mods.384099/

https://www.gtplanet.net/forum/attachments/conversion-of-a-logitech-shifter-for-fanatec-wheelbase-compatibility-by-b-spec-_-bob-dec-2018-pdf.787424/

1 GND
2 low = H-pattern, high = sequential SEQ
3 internally shorted to pin 2
4 X axis (H-pattern); lever push (sequential)
5 Y axis (H-pattern); lever pull (sequential)
6 VCC

```
+---------------------------------------------------------------+
|   6    |   5   |     4      |    3       |    2     |    1    |
| yellow | brown | red,orange | See below  | Not Used |  Black  |
|  WHITE | BLACK |     RED    |   GREEN    |  YELLOW  |   BLUE  |
|  VCC   | Yaxis |    XAxis   | Short pin 2| SEQ      |   GND   | 
+---------------------------------------------------------------+
                           | notch |               
                           +-------+ 

PIN 1 and 3 connected together = H-Pattern shifter
PIN 1 and 3 unconnected = Sequential shifter
```

PIN5 (Y) bajar (I)
PIN4 (X) subir (D)

* When the shifter is in H-pattern mode:
    * SEQ pin is LOW
    * X pin outputs X axis angle (the output from X axis board)
    * Y pin is:
        * VCC if lever is in R/1/3/5/7 (forward)
        * 1/2 VCC if lever is in the center / neutral
        * 0 if lever is in 2/4/6 (backward)

* When the shifter is in Sequential mode:
    * SEQ pin is HIGH
    * X pin goes LOW if the lever is pushed forward (gear 3)
    * Y pin goes LOW if the lever is pulled backward (gear 4)



```
 (6) VCC
  x
  |                         
  |                                 
  +---------[ 10K ]---+-------/ ----------+
  |                   | (5) X             | 
  |                   x                   x (1) GND
  |                                       |         
  +---------[ 10K ]---+------/ -----------+
  |                   | (6) Y               
  |                   x
  |  
  +------x (3) 
  |
  +------x (2) SEQ
  |

  ```

## part list

1. plate
    1.1. reinforcement
2. Lever
    2.1. lever adapter (for the Fanatec BMW GT2 shift paddle)
3. base plate
    3.1. rear cap
4. cap
5. cable box



