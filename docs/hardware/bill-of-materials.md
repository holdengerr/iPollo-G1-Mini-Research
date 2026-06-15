# Bill of Materials

This table lists identified parts or part families with a confidence label.

| Subsystem | Part / marking | Role | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Host board | `ALLWINNER TECH H3` | main SoC | Confirmed | visible package marking |
| Host board | `H5TQ2G63GFR` | DDR3 DRAM | Confirmed | 2 Gbit x16, 256 MB total |
| Host board | `EN25QH128A-104HIP` | SPI NOR flash | Confirmed | 16 MB |
| Host board | `HanRun TF102 2213T` | Ethernet magnetics | High | visible marking, exact vendor doc not yet matched |
| Mining side | `ISL68127` | regulator / PMBus-capable controller | Confirmed | identified from board photo |
| Mining side | `FT24C16A` | I2C EEPROM | High | likely configuration/calibration storage |
| Mining side | `MX25U4033E` | 1.8 V SPI NOR flash | High | 4 Mbit local flash |
| PSU | `HKA150120A0-7C` | external 12 V power adapter | Confirmed | 120 W rated |

## Evidence

- All confirmed entries above come from package markings or direct hardware observation.
- `FT24C16A` and `MX25U4033E` are identified from direct package markings; their exact stock role remains partly inferred.
