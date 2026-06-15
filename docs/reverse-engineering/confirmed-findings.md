# Confirmed Findings

This page collects the highest-confidence results only.

## Hardware

- The host board uses an **Allwinner H3** SoC.
- The host board uses external **DDR3 DRAM**.
- The host board boots from **16 MB SPI NOR** flash.
- The board exposes Linux-visible LEDs for `green:pwr` and `red:status`.

## Stock software

- The device runs an OpenWrt-derived Linux environment.
- Stock userspace includes `cgminer`, `cgminer-api`, and `cgminer-monitor`.
- Stock Linux exposes MTD partitions, serial ports, and I2C buses.

## UART protocol

- The mining link runs at **4,000,000 baud 8N1**.
- Observed frame types are `0x00` through `0x05` as documented in the protocol pages.
- Stock `cgminer` sends `0x05` ACK/NACK in response to `cmd04` result-frame CRC decisions.

## MCU and power control

- MCU firmware writes regulator targets through register `0x21`.
- MCU firmware reads voltage through register `0x8b`.
- Probe firmware confirmed current and power reads through `0x8c` and `0x96`.
- The MCU firmware contains an autonomous up/hold/down frequency adjustment loop based on runtime reset behavior.
