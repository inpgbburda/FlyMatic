# Sending power control from master to slave

## Frame format
Information is send in the following frame format through the SPI:

|    0    |    1    |    2    |    3    |
|---------|---------|---------|---------|
| Power_1 | Power_2 | Power_3 | Power_4 |

Values are in range of uint8 format:

0 - No power requested on corresponding motor  
255 - maximum power requested on corresponding motor

Bytes are sent in ascending order (Power_4 to Power_1)

## Period of sending
Frames are sent from MainUnit to AuxUnit cyclicaly with 10ms period.

## Bus settings
Bus details:  
    - MainUnit is a master of communication.  
    - Motorola mode  
    - first edge of SCK as latching event  
    - low SCK state assummed as idle  
    - 8 bit format of data frame