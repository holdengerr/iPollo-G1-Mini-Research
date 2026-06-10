This document contains observations and reverse engineering notes regarding communication between the controller board and the G22 ASIC hashboard.
This information is based on packet captures, firmware analysis and observation of stock firmware and processes.
Many fields remain unidentified or unclear and should be considered provisional.

UART Interface Specs

Device: /dev/ttyS1 (on stock firmware, untested on others)\
Baud: 4,000,000\
Mode: raw serial\
Echo: off\
Flow ctrl: off\
Config: 8-bit data implied, no software/hardware flow control

Basic Frame Format:

```text
ff 55 FT ...payload... CRC_H CRC_L
|  |  |        |
|  |  |        CRC16-CCITT over bytes from FT through payload
|  |  frame type
|  header
header
```
There are currently 6 known Frame Types:

```text
0x00 Work frame, host-->ASIC
0x01 Command/status response, ASIC-->host
0x02 Algorithm select, host-->ASIC
0x03 Status frame, ASIC-->host
0x04 Mining result frame, ASIC-->host
0x05 ACK/NACK, host-->ASIC
```
