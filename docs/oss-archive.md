# Panasonic OSS archive — obtain & inventory

The Panasonic notice on the unit points to the open-source page:

- `http://car.panasonic.jp/oss/c01vvt13` (as printed on the unit)
- `https://car.panasonic.jp/oss/c01vvt13/`

This hosts the **corresponding source for the open-source components only**
(LGPL v2.1 code, plus ISC-licensed pieces and FreeType). It is **not** the full
Toyota/Panasonic infotainment system, UI, bootloader, or firmware.

## Status in this session

⚠️ **Blocked:** outbound network to `car.panasonic.jp` is not allowed in this
cloud session, so the archive could not be downloaded here. To fetch it,
`car.panasonic.jp` must be added to the environment's allowed network hosts, or
download it manually and place it in `oss/` (git-ignored, see below).

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
