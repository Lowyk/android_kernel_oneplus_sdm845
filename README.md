# fajita kernel — experimental Android 17 patch tree

Experimental kernel with Android 17 patches, primarily made for **[REDACTED]**.

Based on OnePlus's official `oneplus/SDM845_R_11.0` source release (4.9.227) for the OnePlus 6T (`fajita`, SDM845).

## Status

Patching this ~2018-era 4.9 kernel to boot a modern Android 17 userspace, one missing
kernel API at a time. Progress and findings are tracked as patches land here.

### Landed
- Backport `MADV_WIPEONFORK` / `MADV_KEEPONFORK` (mainline `d2cd9ede6e19`) — Android 17's
  bionic libc calls this unconditionally during early `arc4random` init; without it, `madvise()`
  returns `EINVAL` and init dies within microseconds of starting.

More to come as further gaps are found and closed.
