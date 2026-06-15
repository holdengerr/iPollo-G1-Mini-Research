# Power Delivery

This page covers external power, onboard distribution, and regulator telemetry behavior visible in stock hardware and firmware.

## Confirmed

- External PSU observed: `HKA150120A0-7C`
- PSU rating: **12.0 V, 10.0 A, 120 W**
- The controller and mining hardware use multiple onboard DC-DC stages.
- MCU firmware programs regulator targets through PMBus-like register writes.
- Firmware readback uses regulator register `0x8b` for voltage telemetry.

## PMBus-like regulator behavior

### Confirmed register roles

| Register | Role |
| --- | --- |
| `0x21` | target/config write |
| `0x8b` | voltage readback |
| `0x8c` | current readback, confirmed through probe firmware |
| `0x96` | output power readback, confirmed through probe firmware |

### Confirmed device addresses

| Device | Observed purpose |
| --- | --- |
| `0xc0` | ISL Vddr path |
| `0xb4` | second ISL rail path |
| `0x62` | IS6608A-style Vddr path |
| `0x60` | IS6608A-style Vcore path |

## Observed live telemetry

Probe firmware work showed plausible loaded values such as:

| Rail | Observed current | Observed power |
| --- | ---: | ---: |
| DDR rail | `7.7..9.0 A` | about `10 W` |
| Core rail | `48.6..52.9 A` | about `52 W` |

These values were observed through temporary MCU probe firmware rather than the stock Linux userspace.

## Inferred

- The measured PMBus power does not represent total wall power; it likely excludes host-board consumption, fan power, and conversion loss.
- The external ~95 W wall-power observations are consistent with the probed rail figures plus system overhead.

## Unknown

- Full calibration/scaling rules used by stock MCU code for every PMBus telemetry register
- Whether additional rails exist but are not exposed through the currently observed debug path

## Evidence

- Board photo identified `ISL68127`.
- MCU firmware decompilation ties `0x21` writes and `0x8b` readback to named `ISL` voltage paths.
- Temporary probe firmware confirmed readable values at `0x8c` and `0x96`.
