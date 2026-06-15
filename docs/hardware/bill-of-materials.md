# Bill of Materials

This table lists identified parts or part families with a confidence label.

| Subsystem | Part / marking | Role | Confidence | Notes |
| --- | --- | --- | --- | --- |
| Host board | `ALLWINNER TECH H3` | main SoC | Confirmed | visible package marking |
| Host board | `H5TQ2G63...` SK hynix DDR3 | DRAM | High | exact suffix still soft |
| Host board | `EN25QH128A-104HIP` | SPI NOR flash | Confirmed | 16 MB |
| Host board | `HanRun TF102 2213T` | Ethernet magnetics | Confirmed | visible marking |
| Mining side | `ISL68127` | regulator / PMBus-capable controller | Confirmed | identified from board photo |
| Mining side | `FJ2167A 9YJBME` | companion IC near regulator area | Low | function unknown |
| PSU | `HKA150120A0-7C` | external 12 V power adapter | Confirmed | 120 W rated |

## Evidence

- All confirmed entries above come from package markings or direct hardware observation.
- DRAM family and capacity are inferred from the visible SK hynix marking and board topology.
