# Findings — established vs. unverified

## Established (from the project PDF / conversation)

- The car is a **2018 Toyota Corolla** with a Panasonic-built factory multimedia unit.
- System-info screen reads **Device ID `13TFDAEU-DA07`**, **Software `0101B9`**.
- The unit **displays Spotify track metadata over Bluetooth** (title/artist) —
  this confirms standard Bluetooth media integration (A2DP + AVRCP), nothing more.
- A **Panasonic OSS notice** is present. It identifies:
  - LGPL v2.1 components (source offered at `car.panasonic.jp/oss/c01vvt13`).
  - **iAnywhere Blue SDK** (Extended Systems / iAnywhere) — the Bluetooth stack.
  - **FreeType** (font rendering) and **ISC-licensed** components.
- The phone is a **Xiaomi 13T** (Android), intended to do all the processing.

## NOT established (must be proven before trusting)

- The exact **operating system** of this unit (embedded Linux? a real-time OS
  like ITRON/T-Kernel? something else). The OSS notice listing LGPL code does
  **not** prove Linux.
- The exact **CPU / SoC** and hardware revision.
- Whether **USB** supports anything beyond Toyota-signed update packages.
- Whether there is any **developer/service/diagnostic interface**.
- Whether the unit will accept a **custom Bluetooth data channel** (beyond A2DP/AVRCP).
- Whether it can **render any third-party UI**.
- Whether native **Waze / Spotify / WhatsApp** could ever run on it. (Almost
  certainly **no** — it is not Android.)

## Four capabilities that are often confused

These are independent. Evidence for one is **not** evidence for another:

1. **Android Auto support** (projection protocol over USB/Wi-Fi).
2. **Android OS** running on the head unit.
3. **Bluetooth media metadata** (what we already see with Spotify).
4. **Ability to run arbitrary custom code** (what the project actually needs).

Current evidence only supports **#3**.

## Honest assessment

The phone-side dashboard is easy. The blocker is the head unit: it must be able
to *execute custom rendering code* and *receive data over a usable channel*.
Neither is demonstrated, and standard Bluetooth cannot carry arbitrary graphics.
The Panasonic OSS source is a useful lead for understanding libraries and the
Bluetooth stack, but it is **not** the full infotainment OS and does **not**
include an app-launching mechanism.
