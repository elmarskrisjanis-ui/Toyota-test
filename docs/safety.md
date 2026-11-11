# Safety rules (non-negotiable for this phase)

These protect the car. They override any "let's just try it" impulse.

1. **Read-only until proven.** No flashing, patching, or writing to the unit
   until compatibility, a documented install method, **and** a recovery path are
   all demonstrated.
2. **No homemade update media.** Do not insert self-made USB "update" packages.
   If packages are signed (very likely), they'll be rejected; if signing is
   bypassed wrongly, the unit can brick.
3. **Preserve factory software and settings.** No dashboard disassembly, no
   wiring changes, no head-unit replacement — per the project rules.
4. **Firmware update ≠ app install.** Even a working official update mechanism
   does not imply arbitrary code execution.
5. **Recovery first.** Before any write is ever considered, document exactly how
   to restore the unit to stock. No recovery path → no write.
6. **Legal/ownership.** Only investigate hardware you own. The Panasonic OSS
   source is published for compliance; use it for understanding, and respect its
   licenses. Do not redistribute proprietary firmware.

## Decision gate (copy of Phase 4)

Proceed to an in-car write **only if all** are true:
- Verified, documented installation method ✔
- Reliable recovery/un-brick path ✔
- Confirmed package compatibility with this exact unit ✔

Otherwise: **stop**, keep everything on the phone side.
