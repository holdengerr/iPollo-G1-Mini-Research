# UART Protocol

This page covers the transport-level serial protocol observed between the host board and the mining side.

## Transport

**Confirmed**

- Device path on stock Linux: `/dev/ttyS1`
- Baud rate: **4,000,000**
- Framing: **8N1**
- No software or hardware flow control observed

## Frame format

```text
ff 55 FT CN <payload> CRC
|  |  |  |            |
|  |  |  chip number  CRC16-CCITT over FT through payload
|  |  frame type
|  header
header
```

## Known frame types

| Type | Direction | Purpose |
| ---: | --- | --- |
| `0x00` | host -> ASIC | work frame |
| `0x01` | ASIC -> host | work-response / short status |
| `0x02` | host -> ASIC | algorithm select |
| `0x03` | ASIC -> host | status / temperature |
| `0x04` | ASIC -> host | mining result |
| `0x05` | host -> ASIC | ACK/NACK |

## Directionality summary

- The host sends work, algorithm-select, and ACK/NACK frames.
- The mining side sends work-response, status, and result frames.

## Evidence

- Passive UART captures and stock `cgminer` decompilation agree on the frame-type set above.

## Related pages

- [Frame types](frame-types.md)
- [ACK/NACK behavior](ack-nack-behavior.md)
- [Algorithm select](algorithm-select.md)
