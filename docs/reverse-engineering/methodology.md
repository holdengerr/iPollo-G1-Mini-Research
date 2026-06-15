# Methodology

This repository is based on a combination of direct observation and reverse engineering of stock hardware and stock software.

## Methods used

- board photography and package-marking identification
- live Linux inventory from stock or stock-like boot environments
- passive UART capture
- stock `cgminer` decompilation and control-flow tracing
- MCU firmware decompilation and targeted recon
- temporary read-only probe firmware for regulator telemetry confirmation

## Principles

- Prefer direct evidence over assumption.
- Separate confirmed observations from inferences.
- Document uncertainty explicitly when a field, component, or behavior is unresolved.
- Keep custom replacement-software work out of this repository except where stock behavior needs contrast.

## Limits

- Some findings depend on partial decompilation and may improve with better symbols or more captures.
- Not all raw artifacts are published in this repository.

## Evidence

- The source-evidence appendix maps major claims to photos, captures, stock files, or unpublished internal recon notes.
