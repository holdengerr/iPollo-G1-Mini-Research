# Open Questions

This page tracks the main unresolved technical questions.

## ASIC and mining-side hardware

- What is the exact ASIC part number?
- How many internal lanes or mining engines are present?
- Are all exposed connector/header positions used in other product variants?

## UART protocol

- What is the exact meaning of every `cmd04` field?
- What does the per-result numeric field near the end of long result frames represent?
- Are there additional frame values or algorithm codes not yet observed?

## MCU firmware and power

- What is the exact MCU model?
- What is the complete mapping for all PMBus-like device addresses and rails?
- How much of the mining-side adaptive behavior depends on ACK/NACK versus watchdog progress counters?

## Board variants

- Which observed hardware differences are true G1 Mini variants versus shared firmware support for related boards?
