# Fanashifter

Tutorial about how to connect shifters (sequential or H-shaped) on Fanatec Wheel bases. 
Tested with a sequential shifter on CSL elite 1.1. Also the 3D models for the Levers and electronics are provided.
In this example, we can connect directly our shifter levers to port Shifter2, but also works on Shifter1.

## Pinout RJ12 (6P6C)

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

  

  