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
ff 55 FT CN <payload> CRC
|  |  |  |            |
|  |  |  chip number  CRC16-CCITT over bytes FT through payload
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
Work Frame (0x00):

Sent from the host to the ASIC, it contains job data from the stratum to be used by the chip to hash a result. 
```text
ff 55 00 00 | pre_pow | nonce/work id | CRC

ff 55           header
00              frame type
00              chip #
pre_pow         cuckatoo32 job data from stratum
nonce/work id   used to match work frames later
CRC             CRC
```

Command/Status Response Frame (0x01):

Sent from the ASIC to the host, it appears to be a short progress/OK/error frame.
```text
ff 55 01 00 (a1 a1 or f1 f1) CRC

ff 55   header
01      frame type
00      chip #
a1 a1   normal/OK progress signal
f1 f1   error signal
CRC     CRC
```

Algorithm Select Frame (0x02):
```text
ff 55 02 00 (a3 a3 or a4 a4) CRC

ff 55   header
02      frame type
00      chip #
a3 a3   MWC algorithm
a4 a4   GRIN algorithm
CRC     CRC
```

Status Frame (0x03):

Sent from the ASIC to the host, it contains temperature data about the chip.
```text
ff 55 03 00 | temp bytes | CRC

ff 55        header
03           frame type
00           chip #
temp bytes   two-byte chip temp reading
CRC          CRC
```
Notes:
- For example, frame ff 55 03 00 17 11 03 28 would be interpredted as 59.05 C, with 17 11 converting to 5905 in decimal.

Mining Result Frame (0x04):

Sent from the ASIC to the host, it returns hashes from the chip to be submitted to the pool.
```text
ff 55 04 00 | result nonce/id | proof data | CRC

ff 55             header
04                frame type
00                chip #
result nonce/id   indentifier to match with work frame
proof data        work received from the ASIC to be submitted to the pool
CRC               CRC
```

ACK/NACK Frame (0x05):

Sent from the host to the ASIC, letting the ASIC know if the result frame it sent was accepted or rejected.
```text
ff 55 05 00 (a5 a5 or f5 f5) CRC

ff 55   header
05      frame type
00      chip #
a5 a5   indicates ACK frame
f5 f5   indicates NACK frame
CRC     CRC
```
Notes:
- An ACK frame refers to a frame that was accepted or correctly understood by the host. It is a simple response to most frames the ASIC sends and appears to be a metric used to adjust frequencies and voltages on the ASIC internally.
- An NACK frame refers to a frame that is invalid or corrupt. This lets the ASIC know it is producing frames the host cannot interpret or that the work was rejected by the pool for example. These frames also appear to change frequencies and volatges on the ASIC.
