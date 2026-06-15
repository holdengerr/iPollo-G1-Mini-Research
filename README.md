# iPollo G1 Mini Research

Research, documentation, and reverse-engineering notes for the stock iPollo G1 Mini device.

## Scope

This repository documents:

- the physical device and PCB hardware
- stock firmware, boot flow, and software layout
- observed UART protocol behavior between the host board and the mining hardware
- reverse-engineered findings from captures, firmware inspection, and board photos

This repository does not document custom miners, live patches, tuning images, or release engineering for replacement software.

## Current high-confidence findings

- The controller board uses an **Allwinner H3** SoC.
- The controller board appears to use **256 MB DDR3** through a single SK hynix x16 DRAM device.
- The board boots from **16 MB SPI NOR** flash.
- The mining path uses a **4,000,000 baud 8N1 UART** between the host board and the mining side.
- The stock software stack is OpenWrt-based and integrates `cgminer` with an external MCU firmware path.
- PMBus-like regulator control and telemetry behavior is present in the MCU firmware.

## Provisional findings

Some details in this repository remain provisional. Where possible, pages separate **Confirmed**, **Inferred**, and **Unknown** statements explicitly.

## Documentation map

- [Overview](docs/overview.md)
- [Hardware](docs/hardware/host-board.md)
- [Firmware and stock software](docs/firmware/stock-software-overview.md)
- [Protocols](docs/protocols/uart-protocol.md)
- [Reverse-engineering notes](docs/reverse-engineering/methodology.md)
- [Appendices](docs/appendices/terminology.md)

## Hardware

- [Host board](docs/hardware/host-board.md)
- [Hash board](docs/hardware/hash-board.md)
- [Power delivery](docs/hardware/power-delivery.md)
- [Connectors and headers](docs/hardware/connectors-and-headers.md)
- [Bill of materials](docs/hardware/bill-of-materials.md)

## Firmware and stock software

- [Stock software overview](docs/firmware/stock-software-overview.md)
- [Boot and storage](docs/firmware/boot-and-storage.md)
- [OpenWrt layout](docs/firmware/openwrt-layout.md)
- [cgminer integration](docs/firmware/cgminer-integration.md)
- [MCU firmware](docs/firmware/mcu-firmware.md)

## Protocols

- [UART protocol](docs/protocols/uart-protocol.md)
- [Frame types](docs/protocols/frame-types.md)
- [ACK/NACK behavior](docs/protocols/ack-nack-behavior.md)
- [Algorithm select](docs/protocols/algorithm-select.md)

## Reverse engineering

- [Methodology](docs/reverse-engineering/methodology.md)
- [Confirmed findings](docs/reverse-engineering/confirmed-findings.md)
- [Open questions](docs/reverse-engineering/open-questions.md)

## Appendices

- [Terminology](docs/appendices/terminology.md)
- [Source evidence](docs/appendices/source-evidence.md)
