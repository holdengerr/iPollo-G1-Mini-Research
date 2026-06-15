# Frame Types

This page lists the currently documented frame types with concrete examples.

## `0x00` Work frame

Direction: host -> ASIC

```text
ff 55 00 00 | pre_pow | nonce/work id | CRC
```

Purpose: carries job data from the host to the mining side.

## `0x01` Work-response frame

Direction: ASIC -> host

```text
ff 55 01 00 a1 a1 fd 30
ff 55 01 00 f1 f1 ?? ??
```

Observed meanings:

- `a1 a1`: work response OK
- `f1 f1`: work response error

## `0x02` Algorithm-select frame

Direction: host -> ASIC

```text
ff 55 02 00 a3 a3 ...
ff 55 02 00 a4 a4 ...
```

Observed meanings:

- `a3 a3`: MWC algorithm
- `a4 a4`: GRIN algorithm

## `0x03` Status frame

Direction: ASIC -> host

```text
ff 55 03 00 17 11 03 28
```

Observed meaning: two-byte temperature field. The example above was interpreted as about `59.05 C`.

## `0x04` Result frame

Direction: ASIC -> host

```text
ff 55 04 00 | result nonce/id | proof data | CRC
```

Observed behavior:

- carries mining result data
- long-form results are CRC-checked and then ACKed/NACKed by stock `cgminer`
- stock preserves the full raw frame for downstream processing

## `0x05` ACK/NACK frame

Direction: host -> ASIC

```text
ff 55 05 00 a5 a5 bb 81
ff 55 05 00 f5 f5 ef cb
```

- `a5 a5`: ACK
- `f5 f5`: NACK

## Evidence

- Frame examples above come from passive captures and stock parser analysis.
