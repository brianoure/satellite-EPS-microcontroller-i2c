# satellite-EPS-microcontroller-i2c
A satellite Electrical Power Subsystem (EPS) microcontroller program written in Python.<br />
<br />
In this case satellite system, the EPS microntroller communicates with the On Board Computer (OBC) microcontroller using the I2C protocol.<br />
<br />
Each I2C channel requires three lines - 2 signal (i.e SDA and SCL) and 1 ground (GND) hence 2 channels (SDA1, SCL1, SDA2, SCL2 and GND) are implemented to
enable transmission and reception of packets between the OBC and the EPS respective microcontrollers.

As for telemetry data, the EPS outputs a - 56 bit frame - to the OBC sectioned as follows;
| Packet Section                                 | Bit width     | Possible values (Meaning or representation)        |
| -------------                                  | ------------- | --------------                                     |
| Header                                         | 8             | 195(valid frame identifier starting constant)      |
| Payload subsystem state                        | 2             | 1(Payload is ON) or 0(Payload is OFF)              |
| Communication subsystem component (UHF) state  | 2             | 1(UHF is ON)    or 0(UHF is OFF)                   |
| Communication subsystem component (Xband) state| 2             | 1(Xband is ON) or 0(Xband is OFF)                  |
| Solar Panel Array1 output voltage              | 5             | 0 to 32 (integer value for voltage range)          |
| Solar Panel Array2 output voltage              | 5             | 0 to 32 (integer value for voltage range)          |
| Solar Panel Array3 output voltage              | 5             | 0 to 32 (integer value for voltage range)          |
| Solar Panel Array4 output voltage              | 5             | 0 to 32 (integer value for voltage range)          |
| 8 cell Battery voltage (4S2P arrangement)      | 5             | 0 to 32 (integer value for voltage range - for a maximum output of 4V per cell, the highest yield should be 16V) |
| Battery temperature                            | 9             | -255 to 256(valid frame ending identifier constant)|
| Tail                                           | 8             | 135(valid frame ending identifier constant)        |

Whereas the EPS receives a - 48 bit frame - from the OBC that consists of the following information;
| Packet Section                                 | Bit width     | Possible values/ (Meaning or representation)      |
| -------------                                  | ------------- | --------------                                    |
| Header                                         | 16            | 34539(valid frame identifier starting constant)   |
| Payload subsystem state                        | 8             | 197(turn payload ON) or 245(turn payload OFF)     |
| Communication subsystem component (UHF) state  | 8             | 117(turn UHF ON)    or 199(turn UHF OFF)          |
| Communication subsystem component (Xband) state| 8             | 149(turn Xband ON) or 87(turn Xband OFF)          |
| Tail                                           | 8             | 135(valid frame ending identifier constant)       |

