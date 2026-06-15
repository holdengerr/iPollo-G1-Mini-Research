# cgminer Integration

This page describes the stock `cgminer` role only.

## Confirmed

- Stock `cgminer` owns the UART result/work parser path for the mining link.
- It validates framed UART traffic, emits ACK/NACK traffic for result frames, and submits accepted work through the normal cgminer share path.
- It maintains per-lane and per-chip accounting state from result traffic.

## Observed responsibilities

| Responsibility | Evidence |
| --- | --- |
| Parse `cmd01`, `cmd03`, `cmd04` UART frames | decompilation of stock `cgminer` receive path |
| CRC validation | stock receive parser calls CRC helpers before processing |
| Immediate result ACK/NACK | stock emits `0x05` frames after `cmd04` CRC decision |
| Duplicate suppression | stock uses a submit-side duplicate gate derived from result-frame state |
| Share submission | stock passes validated results into normal cgminer submission flow |

## Important stock behaviors

- `cmd01` is receive-only accounting; stock does not respond to it with UART output.
- `cmd04` is queued as a raw full frame before deeper processing.
- Lane bits and per-chip state are preserved and used later.

## Unknown

- Full semantic meaning of every result-field offset
- Full scheduler impact of every `cmd01` state update

## Evidence

- Decompiled `cgminer` work-response and result-frame paths show queueing, validation, ACK/NACK, and submission behavior directly.
