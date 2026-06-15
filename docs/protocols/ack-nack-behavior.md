# ACK / NACK Behavior

This page covers what is currently known about frame type `0x05`.

## Confirmed

- ACK frame:

```text
ff 55 05 00 a5 a5 bb 81
```

- NACK frame:

```text
ff 55 05 00 f5 f5 ef cb
```

- Stock `cgminer` sends ACK/NACK immediately after validating a `cmd04` result-frame CRC.
- Stock does **not** send UART ACK/NACK traffic in response to `cmd01`.

## Inferred

- ACK/NACK affects mining-side accounting or control behavior beyond mere transport acknowledgment.
- The mining side appears to treat these frames as meaningful operational feedback, not just parser-level flow control.

## Unknown

- Whether every NACK class is treated the same on the mining side
- How strongly ACK/NACK contributes to any internal frequency or voltage adaptation

## Evidence

- Stock `cgminer` decompilation shows immediate `0x05` emission in the `cmd04` receive path and no corresponding `cmd01` response path.
