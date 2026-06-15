# OpenWrt Layout

## Confirmed

- The host board runs an OpenWrt-derived Linux environment on ARMv7.
- The software stack uses standard OpenWrt conventions such as:
  - `/etc/init.d`
  - LuCI controller/model paths
  - UCI configuration
  - MTD-backed rootfs and writable data

## Notable stock components

| Component | Observed role |
| --- | --- |
| LuCI | web UI framework |
| UCI | device and miner config storage |
| `cgminer` | stock mining/control userspace |
| `cgminer-api` | API helper |
| `cgminer-monitor` | monitoring/helper binary |

## Linux-visible peripherals

The stock board exposes at least:

- `ttyS` serial ports including `/dev/ttyS1`
- I2C buses
- GPIO and LED interfaces
- MTD partitions

## Inferred

- The stock vendor UI is implemented as a device-specific LuCI customization rather than a fully separate web stack.

## Evidence

- Extracted root filesystem contains LuCI controller and model files under `usr/lib/lua/luci/...`.
- Stock rootfs contains `cgminer` binaries and a dedicated `etc/init.d/cgminer` service.
