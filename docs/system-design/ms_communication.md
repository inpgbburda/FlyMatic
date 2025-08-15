# Sending power control from master to slave

## Frame format
Power requests shall be send in the following frame format through the SPI bus:

|    0    |    1    |    2    |    3    |
|---------|---------|---------|---------|
| Power_1 | Power_2 | Power_3 | Power_4 |

Values are in range of `uint8` format:

0 - No power requested on corresponding motor  
255 - maximum power requested on corresponding motor

Bytes are sent in ascending order (Power_1 to Power_4)

## Period of sending
Frames shall be sent from MainUnit to AuxUnit cyclicaly with `10ms` period.
MainUnit shall be a master of communication.