# Source Evidence

This appendix maps major claims to the kind of evidence behind them.

## Hardware identification

| Claim | Evidence |
| --- | --- |
| Allwinner H3 host SoC | board photo with package marking |
| DDR3 host DRAM | closeup board photo with SK hynix marking |
| 16 MB SPI NOR flash | flash package identification and stock-system observations |
| Host-board silkscreen and board type | board photography |
| ISL68127 mining-side regulator | mining-board photo |
| FT24C16A device on hash board | microscope photo with package marking |
| MX25U4033E device on hash board | microscope photo with package marking |

## Stock software

| Claim | Evidence |
| --- | --- |
| OpenWrt-derived rootfs | extracted stock filesystem layout |
| `cgminer` presence and integration | extracted binaries and init/UI files |
| MTD partition names | live Linux `/proc/mtd` inventory |

## UART protocol

| Claim | Evidence |
| --- | --- |
| 4,000,000 baud 8N1 | passive capture setup and successful decode behavior |
| frame types `0x00..0x05` | captures plus stock parser analysis |
| ACK/NACK byte patterns | captures plus stock transmit path |
| `cmd01`/`cmd04` stock behavior | decompiled stock `cgminer` receive and submit paths |

## MCU and regulator behavior

| Claim | Evidence |
| --- | --- |
| regulator target writes at `0x21` | MCU firmware decompilation |
| voltage readback at `0x8b` | MCU firmware decompilation |
| current/power probing via `0x8c`/`0x96` | temporary probe firmware and debug output |
| autonomous frequency control loop | MCU firmware decompilation |

## Notes

- Not every raw artifact used during investigation is published in this repo.
- Where unpublished intermediate material was used, the claim is still limited to what could be verified directly from a stock file, capture, or board observation.
