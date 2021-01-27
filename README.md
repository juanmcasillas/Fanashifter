# Fanashifter

Project about how to connect shifters (sequential or H-shaped) on Fanatec Wheel bases, using it's internal
protocol. Tested with a sequential shifter on CSL elite 1.1. Also the 3D models for the Levers and electronics are provided.
In this example, we can connect directly our shifter levers to port Shifter2 (rj12) also works on Shifter1.

# Table Of Contents

1. [Project Features](#project-features)
2. [3D Printing and Assembly](#3d-printing-and-assembly)
    1. [Plate](#plate)
    2. [Reinforcements](#reinforcements)
    3. [Lever](#lever)
    4. [Lever adapter](#lever-adapter)
    5. [Base plate](#base-plate)
    6. [Rear Cap](#rear-cap)
    7. [Cable box](#cable-box)
    
3. [Mounting](#mounting)    
4. [Fanatec Protocol](#protocol)
5. [Pinout](#pinout)


## Project Features

1. Fully printable, so you can download the project, start your printer, and print all the parts. The STL are 
ready to print, so the orientation and tolerances are configured and tested.
2. Uses the standard RJ12 port with it's internal protocol, so just plug and play.
3. Cheap to build. Based on standard hardware components:
    * Printed on PETG
    * Some wiring cable (8 wires)
    * 30 allen screws (13mm)
    * 4 allen screws (6mm)
    * 2 allen screews M4 (24 mm) for lever axes
    * 2 standard micro switch NO 
    * a RJ12 to RJ12-6p6c (all poles connected, 1-1) cable, to do the wiring.
    * 2 springs for the levers.
    

# 3D Printing and Assembly

All the parts are designed on Autodesk Inventor 2019. I provide the STL files. Printed on a Creality Ender-3 Pro, 
with BQ PETG. These are the CURA settings for all the parts printed:

* Layer Height: 0.2
* Wall Thickness: 0.8
* Top/Botton Thickness: 0.8
* Top Layers: 4
* Bottom Layers: 4
* Infill: 60%, Grid
* Printing temperature: 220 ºC 
* Build plate temperature: 80 ºC
* Speed: 50 mm/s
* Cooling: Enable
* Fan Speed: 100%
* Enable supports: Everywhere
* Build Plate adhesion: None

Note that all the parts are sturdy and the print time is about 3 hours for the plate. Let the printed print. Check
that the nozzle in clean (run small batches) because the PETG is very sticky and stringy.

## Plate

<img src="images/cad/base_plate.png" height="400px">

## Reinforcements

## Lever

## Lever Adapter

## Base Plate

## Rear Cap

## Cable Box


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





