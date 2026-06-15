# Algorithm Select

This page covers frame type `0x02`.

## Confirmed

The host sends an algorithm-select frame with one of two currently observed payloads:

```text
ff 55 02 00 a3 a3 ...
ff 55 02 00 a4 a4 ...
```

Observed mapping:

| Payload | Meaning |
| --- | --- |
| `a3 a3` | MWC |
| `a4 a4` | GRIN |

## Inferred

- The protocol and mining-side firmware were designed to support more than one algorithm family under the same general control path.

## Unknown

- Exact expansion of `MWC` in the vendor implementation
- Whether additional algorithm codes exist but were not observed in available captures
- Whether algorithm-select changes only mining logic or also the framing/validation path for result data

## Evidence

- Passive captures and stock-miner observation both showed `a3 a3` and `a4 a4` algorithm-select traffic.
