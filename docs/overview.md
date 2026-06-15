# Overview

The iPollo G1 Mini is a small Grin-focused mining device built around a Linux-capable black host board and a separate green hash board driven over a high-speed UART link.

## Summary

**Confirmed**

- The controller board uses an **Allwinner H3** SoC.
- The controller board uses external **DDR3 DRAM** and **SPI NOR flash**.
- The host-to-mining path uses a **4,000,000 baud 8N1 UART**.
- The stock system is OpenWrt-based and uses `cgminer` plus an external MCU firmware path.
- Stock software exposes LEDs, serial ports, SPI NOR MTD partitions, and I2C buses.

**Inferred**

- The controller PCB appears to be based on a reusable H3 reference-style board adapted for this product family.
- The mining-side board likely supports more than one regulator or board variant under a common firmware base.

**Unknown**

- Exact ASIC part identity
- Whether all apparent board-to-board connector positions are populated in other variants
- Full meaning of every UART result-frame field

## Major subsystems

- **Host board**: Allwinner H3 SoC, DDR3 DRAM, SPI NOR, Ethernet, stock OpenWrt userspace
- **Mining-side logic**: separate MCU firmware and ASIC-side UART result/status behavior
- **Power delivery**: external 12 V supply, onboard DC-DC stages, PMBus-like regulator control
- **Protocol layer**: framed serial protocol with work, status, result, ACK/NACK, and algorithm-select traffic

## Where to read next

- [Host board](hardware/host-board.md)
- [Power delivery](hardware/power-delivery.md)
- [Stock software overview](firmware/stock-software-overview.md)
- [UART protocol](protocols/uart-protocol.md)
- [Confirmed findings](reverse-engineering/confirmed-findings.md)
