# Read-only firmware research plan

The whole point of this phase: **learn as much as possible without writing
anything to the car.** Every step below is observation or offline analysis.

## Phase 0 — Identify the unit precisely

- [ ] Photograph every system-info / version / diagnostic screen available from
      the factory menus (no service mode needed).
- [ ] Record Device ID (`13TFDAEU-DA07`) and Software (`0101B9`) exactly.
- [ ] Note the region code embedded in the ID (`EU`) — matters for which OSS
      archive and update packages correspond.
- [ ] Cross-reference the ID against public Touch 2 / Touch 2 with Go references
      to confirm the exact variant and generation.

## Phase 1 — Obtain the legally-published source (offline analysis only)

The Panasonic OSS archive is **only** the open-source components (LGPL/ISC),
not the whole system. But it still tells us a lot. See
[`oss-archive.md`](oss-archive.md) for how to fetch and inventory it.

What to extract from the archive, purely by reading files:

- [ ] **Target architecture** — look at toolchain names, cross-compile flags,
      `CFLAGS`, configure scripts (`--host=`, `--target=`), ELF notes in any
      prebuilt `.o`/`.a` if present. ARM vs. SH vs. MIPS tells us the CPU family.
- [ ] **OS hints** — references to `linux`, `uClibc`/`glibc`, `itron`, `t-kernel`,
      `vxworks`, BSP directory names, init scripts.
- [ ] **Bluetooth stack** — the iAnywhere Blue SDK headers/usage: which profiles
      are compiled in (A2DP, AVRCP, HFP, SPP, PBAP, MAP...). **SPP (Serial Port
      Profile)** would be the most interesting — it's the only standard profile
      that could carry a custom data channel.
- [ ] **Build system** — Makefiles, Yocto/Buildroot/OpenEmbedded recipes, which
      would strongly imply embedded Linux.
- [ ] **FreeType version/config** — confirms the text/graphics rendering path.

> ⚠️ The archive will almost certainly **not** contain the proprietary UI,
> bootloader, application launcher, or signing keys. Do not expect a path to run
> code to fall out of it. We read it to understand the platform, not to unlock it.

## Phase 2 — Understand the update mechanism (still no writing)

- [ ] Find the documented Toyota map/firmware **USB update procedure** for this
      generation (official instructions only).
- [ ] Determine the **update package format** and whether packages are
      **cryptographically signed**. If signed (very likely), homemade packages
      will be rejected — which is the main wall for custom code.
- [ ] Treat a *firmware update* as completely different from *installing an app*.
      The unit supporting updates does **not** mean it runs arbitrary software.

## Phase 3 — Look for any sanctioned execution path

- [ ] Is there a documented **developer mode, service menu, or diagnostic
      interface**? (Read-only: just check whether one is reachable, don't abuse it.)
- [ ] Does the unit support **MirrorLink** or any projection standard that a
      phone app can legitimately target? (This is the most realistic "custom-ish"
      path and needs confirmation for this exact variant.)
- [ ] Separately, investigate whether a **custom Bluetooth SPP channel** is even
      accepted by the unit. Spotify metadata working only proves A2DP/AVRCP.

## Phase 4 — Decision gate

Only consider *any* in-car write/flash if **all** of these are true:

1. A verified, documented installation/update method exists.
2. A reliable **recovery path** exists (how to un-brick).
3. Compatibility of the specific package with this exact unit is confirmed.

If any is missing → **stop**. Keep the project on the phone side.

## Realistic outcome

Most likely conclusion: this unit cannot run custom code through any safe,
documented path, and Waze cannot run on it. The valuable, low-risk deliverable
remains the **phone-side dashboard** on the Xiaomi 13T. We proceed with the
research to *prove* the limitation rather than assume it — and we stop at the
decision gate.
