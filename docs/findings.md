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

## Established from the Panasonic OSS archive (new — 2026-11-11)

Fetched and inspected the official notice at
`https://car.panasonic.jp/oss/c01vvt13/` and its one source download.

- **Operating system: almost certainly embedded Linux.** The only LGPL source
  Panasonic publishes for this product is **`asound.zip` = alsa-lib** (ALSA, the
  *Advanced **Linux** Sound Architecture* user-space library; inspected files are
  classic ALSA `pcm/`, `mixer/`, `control/` code, `SND_LIB_VERSION` ~0.5.2, an
  old 2001-era release). ALSA is Linux-specific — shipping alsa-lib is a strong
  indicator the head unit runs a Linux kernel. (Not ITRON/T-Kernel, WinCE, QNX
  or VxWorks — none are referenced.)
- **Supporting evidence:** the category-(4) notice is a large embedded
  networking/crypto stack — hundreds of **OpenSSL**, **ISC**, **MIT** and
  **BSD/NetBSD/OpenBSD** (ppp, IPv6CP/RFC2472, pf, ALTQ) notices — typical of a
  Linux-based automotive platform, not a thin RTOS.
- **But: this does not open a path to run apps.** The archive is *libraries
  only*. There is **no** UI, bootloader, init system, application launcher, or
  signing key here — i.e. nothing that lets custom code be loaded or run. Linux
  underneath ≠ able to install software. The system is locked down by Toyota/
  Panasonic's proprietary layer, which is **not** published.

## Still NOT established (must be proven before trusting)

- The exact **CPU / SoC** and hardware revision (OSS text mentions ARM in
  passing; not confirmed for this unit).
- Whether the `c01vvt13` notice corresponds **exactly** to device
  `13TFDAEU-DA07` / software `0101B9`, or to a close sibling in the same family.
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

Current evidence supports **#3**, and now points to a **Linux kernel**
underneath (capability adjacent to #2 but *not* Android, and *not* #4). There is
still **no evidence for #4** — the ability to run arbitrary custom code — and the
published source contains nothing that would provide it.

## Honest assessment

The phone-side dashboard is easy. The blocker is the head unit: it must be able
to *execute custom rendering code* and *receive data over a usable channel*.
Neither is demonstrated, and standard Bluetooth cannot carry arbitrary graphics.
The Panasonic OSS source is a useful lead for understanding libraries and the
Bluetooth stack, but it is **not** the full infotainment OS and does **not**
include an app-launching mechanism.
