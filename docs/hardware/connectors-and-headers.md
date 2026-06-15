# Connectors and Headers

This page records visible connectors and exposed debug points.

## Confirmed

- Ethernet port on the host board
- Three large right-side board-to-board connectors on the host board
- Four 4-pin Mini-Fit style power/output connectors in the lower-right power area
- One larger 6-pin power connector footprint/position near `CN1`
- Mining-side debug/test labels observed on the board family include:
  - `SCL`, `SDA`
  - `TX1`, `RX1`
  - `TX2`, `RX2`
  - `EN1`, `EN2`, `EN3`
  - `FG1`..`FG4`
  - `PWM_P1`..`PWM_P4`
  - `DC_IN`
  - multiple `TP` test pads

## Linux-visible interfaces

On the stock software side, the platform exposes:

| Interface | Observed nodes |
| --- | --- |
| UART | `/dev/ttyS0`, `/dev/ttyS1`, and additional `ttyS*` nodes |
| I2C | `/dev/i2c-0`, `/dev/i2c-1`, `/dev/i2c-2` |
| GPIO | `gpiochip0`, `gpiochip1` |
| LEDs | `green:pwr`, `red:status`, `reset1`, `reset2`, `reset3` |

## Inferred

- The three large right-side board-to-board connectors likely carry the host-to-mining interconnect rather than general-purpose IO.
- The exposed TX/RX/EN labels suggest factory bring-up, line control, or multi-lane probing access.

## Unknown

- Final signal map for every pin on the large board-to-board headers
- Whether the extra TX/RX/EN-labelled positions represent alternate board variants or unused lane access in this unit

## Evidence

- Board photography shows the host-board power and interconnect layout directly.
- Mining-side board photography shows the labelled debug/test pads.
