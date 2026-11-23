# fajita kernel — experimental modern-Android patch tree

Experimental kernel patches for running a modern Android userspace on the
OnePlus 6T (`fajita`, SDM845).

**Current target:** StepAOS (StepFun's Android 16-based OS).
**Previous target:** ColorOS 17 (Android 17), now paused.

Based on OnePlus's official `oneplus/SDM845_R_11.0` source release (4.9.227).

## Status

### StepAOS (current)
Work in progress. First step: squashfs support, because the kernel has no
EROFS and the fajita system partition is a fixed ~2.8 GiB.

### ColorOS 17 (previous, paused)
Booted, but most hardware, including the display, did not work. The display
failure is thought to be an Android 17 quirk. On hold until later.

## Landed
- Backport `MADV_WIPEONFORK` / `MADV_KEEPONFORK` (mainline `d2cd9ede6e19`).
  Android 17's bionic libc calls it unconditionally during early `arc4random`
  init; without it `madvise()` returns `EINVAL` and init dies within
  microseconds of starting.
- `LOCALVERSION` cleared, since a suffix was suspected of breaking init's
  uname-based kernel version parsing.
- `BLK_DEV_LOOP_MIN_COUNT` raised from 16 to 48 to fit all 34 APEX loop mounts.
- Enable squashfs (xattr, lz4, xz) for compressed read-only system images on a
  kernel without EROFS.
