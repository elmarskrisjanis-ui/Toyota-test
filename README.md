# Toyota Touch 2 (Panasonic) — Read-Only Firmware Research

**Vehicle:** 2018 Toyota Corolla sedan
**Head unit:** Panasonic-built Toyota Touch 2 family
**Device ID:** `13TFDAEU-DA07`
**Software version:** `0101B9`
**Goal:** Investigate whether this factory multimedia unit can run custom code
(ultimately a Waze / Spotify / WhatsApp dashboard driven by a Xiaomi 13T),
**without modifying the car** at this stage.

> ⚠️ **This repository is research only.** Nothing here flashes, patches, or
> writes anything to the car. The hard rule is: **read and understand first,
> change nothing until compatibility, install method, and recovery are all
> proven.** See [`docs/safety.md`](docs/safety.md).

## Reality check

This unit runs Panasonic/Toyota's own closed embedded firmware, not Android.
There is **no published, confirmed way to run arbitrary apps on it**, and the
USB port is designed only for Toyota-signed map/firmware updates. So the honest
status is: *unproven, probably not possible without significant reverse
engineering, and genuinely risky if firmware is written.* This project exists to
replace guesses with evidence — safely.

## What this repo is for

1. Collect and inventory the **Panasonic open-source (OSS) archive** for this
   unit — which is legally published source for the LGPL/ISC components only.
2. Document the **hardware/software identity** so we know exactly what we're
   dealing with.
3. Map out a **read-only investigation plan** (what to look at, in what order).
4. Hold a **phone-side prototype** (the Waze/Spotify/WhatsApp dashboard) that can
   be built and tested entirely on the Xiaomi 13T, independent of the car.

## Layout

- [`docs/findings.md`](docs/findings.md) — established vs. unverified facts.
- [`docs/firmware-research.md`](docs/firmware-research.md) — read-only research plan.
- [`docs/oss-archive.md`](docs/oss-archive.md) — how to obtain & inventory the Panasonic OSS source.
- [`docs/safety.md`](docs/safety.md) — the rules that keep the car intact.
- [`docs/leads.md`](docs/leads.md) — external references to confirm.

## Current status

- [x] Hardware/software identifiers recorded
- [x] Panasonic OSS archive downloaded & inventoried (`asound.zip` = alsa-lib)
- [x] Head-unit OS inferred from evidence: **embedded Linux** (ships ALSA) — see `docs/findings.md`
- [ ] Head-unit CPU/SoC confirmed
- [ ] Update-package format understood
- [ ] Any safe code-execution path identified (none so far — published source is libraries only)
- [ ] Phone-side prototype built

**Key result so far:** the unit almost certainly runs embedded Linux, but the
published open-source is *libraries only* — no UI, bootloader, or app launcher —
so it provides **no path to run custom code**. Linux underneath ≠ able to
install apps.
