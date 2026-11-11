# MirrorLink on Toyota Touch 2 — inspection

Source: DIMI's firsthand research, "Toyota touch 2 & MirrorLink 1.0 research"
(shafr.github.io, 2 Aug 2021). Fetched & read 2026-11-11. Treat as a credible
hobbyist report, not official Toyota documentation, but it is detailed and
hands-on.

## What MirrorLink is

- A phone-to-head-unit **screen projection** standard — "like VNC that transfers
  screen data." The **phone is the server, the head unit is the client**.
- Runs over a **USB cable** (not Bluetooth).
- It mirrors the **phone's screen**; it is *not* a way to run code on the head
  unit. The Touch 2 is only a MirrorLink **client/viewer**.

## The hard constraint: Touch 2 = MirrorLink **1.0 only**

- Per forums + the official user manual, **Toyota Touch 2 supports MirrorLink
  1.0 only**. Versions went 1.0→1.3; if phone and HU MirrorLink versions differ,
  they won't pair and no menu appears.
- **MirrorLink 1.0 only existed on phones with Android < 4.3.** The author's
  phrase: "exactly 2.5 devices are supported." Known-working phones:
  - **Samsung Galaxy S3**
  - **Nokia 701, N8, N9**
  - some **Sony Xperia** models
- The server app is Samsung **Drive Link** (installs `TMServerApp.apk` in
  `/system/app` and `app.scm.apk` in `/data/app`).

## What actually worked (and didn't)

- On a **Galaxy S3** (old Android, custom ROM `Android_Revolution_HD-SGS3`), Drive
  Link launched, connected over USB, and the **DriveLink menu appeared on the
  Touch 2**. Phone screen was mirrored.
  - Of the stock apps, **only Waze & Google Maps worked**.
  - A **cracked DriveLink** (from the 4pda forum) removes the app whitelist and
    lets you mirror **any** app, even the desktop.
- On a **newer phone (Galaxy A3, Android 6.0)** the car menu appeared only once
  and **would not start properly** — Android logs showed **missing libraries in
  `/lib/arm`**. In short: modern Android ≠ MirrorLink 1.0 server.

## What this means for THIS project (Xiaomi 13T)

- ❌ **The Xiaomi 13T cannot be the MirrorLink source.** It runs modern Android
  (13/14), far beyond the Android < 4.3 that MirrorLink 1.0 DriveLink requires.
  The A3-on-Android-6 failure already shows modern Android breaks it.
- ⚠️ **It also conflicts with the project's stated design:**
  - MirrorLink is **USB**, but the project wanted **Bluetooth**.
  - MirrorLink is **full-screen mirroring** (VNC-style), but the project wanted a
    **compact custom car dashboard rendered on the Toyota**, not a mirror.
  - **No custom code runs on the head unit** — it's just a viewer. So this does
    not unlock "run Waze on the unit"; it streams a phone's screen to it.
- ✅ **The one genuinely usable outcome:** if you buy/borrow an **old Android <4.3
  phone (e.g. a Galaxy S3)**, install Drive Link + (optionally cracked DriveLink),
  and connect it **by USB**, you can get **Waze mirrored onto the Touch 2 screen
  today** — no car modification, factory software intact. But it's that old phone
  doing the work, not your 13T, and it's a mirror, not a custom UI.

## The "Android box behind the screen" note

The article also mentions people fitting a **car-android-box behind the screen**
(in the empty GPS-module slot) and launching it via the GPS button. That is
**extra hardware installed inside the dash** → it breaks the project's rules
(no head-unit replacement, no dashboard disassembly) and is out of scope here.

## Verdict

MirrorLink is the only "phone content on the Touch 2 screen" path that doesn't
touch the car — but on **Touch 2 it's 1.0-only**, which locks it to **ancient
Android phones over USB**, as **full mirroring**. It cannot be driven by the
Xiaomi 13T and does not deliver the custom Bluetooth dashboard the project set
out to build. Useful as a "get Waze on the screen with an old phone" trick;
**not** a route to the original goal.
