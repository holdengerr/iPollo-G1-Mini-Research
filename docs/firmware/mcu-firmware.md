# MCU Firmware

This page covers the stock mining-side MCU firmware family, including `Mini-G22` images and loader variants.

## Confirmed

- The mining side uses a separate MCU firmware path from the Linux host userspace.
- Firmware performs regulator configuration and readback through PMBus-like register access.
- Firmware contains autonomous frequency/DDR adjustment logic based on runtime stability signals.

## Autonomous controller behavior

High-confidence decompilation shows:

| Recent watchdog reset count | Action |
| ---: | --- |
| `0` or `1` | step frequency/DDR up |
| `2` or `3` | hold |
| `4+` | step frequency/DDR down |

This logic is driven by a no-progress watchdog on a mining progress counter rather than directly by pool accept statistics.

## Regulator behavior

- firmware writes regulator target values through register `0x21`
- firmware reads output voltage through register `0x8b`
- probe firmware confirmed readable current and power telemetry through `0x8c` and `0x96`

## Inferred

- The firmware base likely supports multiple board or regulator populations.
- Runtime settling at specific DDR values can be explained by the MCU's closed-loop search behavior.

## Unknown

- Exact MCU model
- Full meaning of all PMBus-like device addresses and any hidden rail mappings

## Evidence

- Decompiled MCU control loop shows explicit increment/hold/decrement behavior.
- Voltage-control and telemetry paths are visible in firmware helper calls and confirmed by temporary probe images.
