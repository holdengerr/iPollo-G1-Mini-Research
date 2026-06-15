# Stock Software Overview

The stock device runs an OpenWrt-based Linux userspace on the host board and interacts with a separate mining-side MCU firmware.

## Confirmed

- The stock userspace is OpenWrt-derived.
- The stock miner path uses `cgminer`.
- The device exposes a LuCI-style web UI and device-specific pages.
- The mining stack depends on both Linux userspace and a separate MCU firmware image set.

## Major layers

| Layer | Role |
| --- | --- |
| Bootloader and kernel | boots the Allwinner H3 host board |
| OpenWrt root filesystem | networking, web UI, init scripts, config |
| `cgminer` | stock mining/control userspace |
| MCU firmware (`Mini-G22` and loader variants) | mining-side initialization, control, voltage/frequency logic |

## Out of scope

This repository does not document custom replacement miners or modified runtime images except where needed to explain stock behavior by contrast.

## Evidence

- Extracted stock rootfs contains `cgminer`, `cgminer-api`, and `cgminer-monitor`.
- Stock filesystem and live observations show OpenWrt-style init, LuCI, UCI, and MTD layout.
