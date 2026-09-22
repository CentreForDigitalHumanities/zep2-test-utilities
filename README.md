# test scripts

# Enumerate monitors using ZEP

This script enumerates the monitors using ZEP-2.x. It prints some basic information
about the heads. This script also displays a window on each of the heads (up to 6
heads at the moment).

This script makes it possible to ignore setting a window on certain heads.

e.g.
```bash
zep-2.7 enummonitors.zp --i 2
zep-2.7 enummonitors.zp --ignore-heads 23
```

One of the short commings of zep is that it doesn't display which head is the primary.

