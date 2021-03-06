# EWYQ005ADVP protocol data format

For the Daikin air heat pump EWYQ005ADVP, the following for data packet format was observed.

**CRC Checksum**

The CRC checksum is calculated using an 8-bit LFSR with a feed of 0x00 and a generator value of 0xD9.

# Main package

#### 1. Packet "000010..."

| Byte nr       | Hex value observed            | Description           | Data type     | Bit: description |
|---------------|:------------------------------|:----------------------|:--------------|:-----------------|
|     1         | 00                            | Request               | u8
|     2         | 00                            | no end-of-package     | u8
|     3         | 10                            | packet type 10        | u8
|     4         | 00/01                         | Power                 | flag8 | 0: power (off/on)
|     5         | 01/02                         | Operating mode        | flag8 | 1: Heating 2: Cooling
|     6         | 00                            | ?                     | 
|     7         | 36                            | Target heating temp   | f8/8
|     8         | 05/00                         | Automatic mode        | u8 | 0: off 5: on
|     9         | 0F                            | Target cooling temp   | f8/8
|    10         | 00                            | ?                     |
|    11         | 30                            | ?                     |
|    12         | 00                            | ?                     |
|    13         | 00/01                         | Quiet mode            | flag8 | 1: on 0: off
|    14         | 00                            | ?                     | 
|    15         | 00                            | ?                     |
|    16         | 00                            | ?                     |
|    17         | 00/01                         | Test mode             | flag8 | 1: on 0: off
|    18         | XX                            | CRC checksum          | u8


#### 2. Packet "400010..."

| Byte nr       | Hex value observed            | Description           | Data type     | Bit: description |
|---------------|:------------------------------|:----------------------|:--------------|:-----------------|
|     1         | 40                            | Response              | u8
|     2         | 00                            | no end-of-package     | u8
|     3         | 10                            | packet type 10        | u8
|     4         | 00/01                         | Power                 | flag8         | 0: power (off/on) |
|     5         | 00                            | ?                     | 
|     6         | 01/02                         | Operating mode        | flag8         | 1: Heating 2: Cooling
|     7         | 00                            | ?                     |
|     8         | 36                            | Target heating temp   | f8/8
|     9         | 05/00                         | Automatic mode        | u8 | 0: off 5: on
|    11         | 0F                            | Target cooling temp   | f8/8
|    12         | 00                            | ?                     | 
|    13         | 01                            | ?                     |
|    14         | 00/01                         | Quiet mode            | flag8 | 1: on 0: off
|    15         | 00                            | ?
|    16         | 00                            | ?
|    17         | 00                            | Quiet mode            | flag8         | 2: quiet mode (off/on) |
|    18         | 00                            | ?
|    19         | 00/80                         | ? 
|    20         | 07/08/09/0B                   |  mode                 | flag8         | 2: compressor (off/on) 
|    21         | 00                            | ?
|    22         | 00                            | ?
|    23         | 01                            | ?
|    24         | XX                            | CRC checksum          | u8


## communication example

logfile from the bus, some unknown packets:

21:07:04.087 -> 0.026: 000011 CRC=48\
21:07:04.087 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:04.127 -> 0.026: 000020 CRC=83\
21:07:04.167 -> 0.024: 4000200314053719501901953E40323C0032010F0001 CRC=D1\
21:07:04.207 -> 0.026: 00001001010036000A0030000000000000460A CRC=B4\
21:07:04.247 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44\
21:07:04.327 -> 0.026: 000011 CRC=48\
21:07:04.327 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:04.367 -> 0.026: 000120 CRC=77\
21:07:04.527 -> 0.130: 00001001010036000A0030000000000000460A CRC=B4\
21:07:04.567 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44\
21:07:04.607 -> 0.026: 000011 CRC=48\
21:07:04.647 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:04.687 -> 0.026: 808000 CRC=12\
21:07:04.807 -> 0.131: 00001001010036000A0030000000000000460A CRC=B4\
21:07:04.847 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44\
21:07:04.927 -> 0.026: 000011 CRC=48\
21:07:04.927 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:04.967 -> 0.026: 000020 CRC=83\
21:07:05.007 -> 0.024: 4000200314053719501901953E40323C0032010F0001 CRC=D1\
21:07:05.047 -> 0.026: 00001001010036000A0030000000000000460A CRC=B4\
21:07:05.087 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44\
21:07:05.167 -> 0.026: 000011 CRC=48\
21:07:05.167 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:05.207 -> 0.026: 000120 CRC=77\
21:07:05.367 -> 0.127: 00001001010036000A0030000000000000460A CRC=B4\
21:07:05.407 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44\
21:07:05.447 -> 0.026: 000011 CRC=48\
21:07:05.487 -> 0.024: 4000110709E9DFB432 CRC=9D\
21:07:05.527 -> 0.026: 808000 CRC=12\
21:07:05.647 -> 0.131: 00001001010036000A0030000000000000460A CRC=B4\
21:07:05.687 -> 0.024: 4000100100010036000A000100000000008007000001D1 CRC=44
