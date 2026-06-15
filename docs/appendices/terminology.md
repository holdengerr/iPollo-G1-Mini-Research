# Terminology

| Term | Meaning in this repository |
| --- | --- |
| Host board | the Linux-capable controller board built around the Allwinner H3 |
| Hash board | the mining-side board containing regulator and ASIC-side logic |
| MCU firmware | the non-Linux firmware that manages mining-side control behavior |
| Stock software | vendor-shipped software and firmware only |
| Lane | the logical result/work path identifier seen in stock parsing and captures |
| Work frame | host-to-mining job frame, type `0x00` |
| Result frame | mining-to-host share/proof frame, type `0x04` |
| ACK/NACK | host response frame, type `0x05` |
| PMBus path | the observed register-level regulator control/readback path used by MCU firmware |
