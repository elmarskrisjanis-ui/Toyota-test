# Panasonic OSS archive — obtain & inventory

The Panasonic notice on the unit points to the open-source page:

- `http://car.panasonic.jp/oss/c01vvt13` (as printed on the unit)
- `https://car.panasonic.jp/oss/c01vvt13/`

This hosts the **corresponding source for the open-source components only**
(LGPL v2.1 code, plus ISC-licensed pieces and FreeType). It is **not** the full
Toyota/Panasonic infotainment system, UI, bootloader, or firmware.

## Status in this session

✅ **Fetched & inventoried (2026-11-11).** `https://car.panasonic.jp/oss/c01vvt13/`
loaded (HTTP 200). The page is a compliance notice; the **only source download
offered is `asound.zip`** (the LGPL component).

What it is: **alsa-lib** (ALSA user-space sound library) — 20 C files under
`pcm/`, `mixer/`, `control/`, `pcm/plugin/`, header `asoundlib.h`,
`SND_LIB_VERSION` ~0.5.2 (an old ~2001 release). ALSA is **Linux-specific**, so
this is strong evidence the unit runs embedded Linux.

The category-(4) list is a large body of OpenSSL / ISC / MIT / BSD (NetBSD,
OpenBSD: ppp, IPv6CP, pf, ALTQ) notices — a typical embedded Linux networking/
crypto stack.

**Not present in the archive:** any UI, bootloader, init system, application
launcher, or signing keys. So it explains the *platform*, not a way to run apps.
`asound.zip` is saved under `oss/` locally (git-ignored).

## How to fetch (manual, when you can reach the site)

1. Open `https://car.panasonic.jp/oss/c01vvt13/` in a browser.
2. Match the archive to **this unit** (region `EU`, device `13TFDAEU-DA07`,
   software `0101B9`). If several are listed, pick the one whose product/version
   corresponds; record which one.
3. Download the archive(s) to a **new empty directory** `oss/` at the repo root.
4. Verify any provided checksums.

> Downloaded archives are untrusted data. Extract each into its own empty
> subdirectory and never run build tools or interpreters from inside it — pass
> file paths as arguments instead.

## Inventory checklist (offline, read-only)

Once extracted, record the answers in `docs/findings.md`:

- [ ] Top-level component list (which libraries, which versions).
- [ ] Any `configure`/`Makefile`/recipe showing `--host=` / `--target=` /
      `CROSS_COMPILE=` → **CPU architecture**.
- [ ] Presence of Buildroot/Yocto/OpenEmbedded recipes → likely **embedded Linux**.
- [ ] iAnywhere Blue SDK headers → **Bluetooth profiles** compiled in (look for
      SPP especially).
- [ ] FreeType version + build config → rendering path.
- [ ] Any strings referencing the OS, init system, or BSP.

## Suggested local layout (not committed)

```
oss/                 # raw downloads + extractions — git-ignored
  <archive>.tar.gz
  <archive>/         # extracted, read-only analysis
```

`oss/` is in `.gitignore` because the archives are large and are third-party
redistributable source, not our work. Keep only our *notes* in `docs/`.
