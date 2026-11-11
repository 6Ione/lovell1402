# Afterglow 14.02 preflight/status test build

Purpose: improve observability without changing the kernel trigger, patch table, gadget table, or exploit sequence.

## Changes

- `jb-g.js`: records structured preflight PASS/BLOCKED; does not label a preflight as jailbreak completion.
- `jb-g.js`: captures `runAfterglow()` result and displays success only when it returns its completion interface; exceptions/failures display failure.
- `afterglow-g.js`: renames the RWX mapping guard result to a userland observation. If mmap+mprotect succeeds, it logs `GUARD-TRIPPED` and stops safely. It does not assume kernel patch state and does not bypass the guard.

## Test URL

`https://6ione.github.io/lovell1402/launch.html?log=1&afterglow=probe`

Expected diagnostic result:

- `AG-PREFLIGHT-PASS` or `AG-PREFLIGHT-BLOCKED` appears in the log.
- The page must not report `JAILBREAK COMPLETE` or imply that a kernel exploit was attempted.
- The probe is intended to remain non-triggering. Close the PS4 browser after recording the output so held diagnostic descriptors are released.

## Important limitation

This is a preflight and status-reporting test, not a kernel exploit test. It deliberately does not remove or bypass the conservative RWX guard. A successful probe does not prove that Afterglow's kernel exploit works on firmware 14.02.

## Files

Replace only `jb-g.js` and `afterglow-g.js` in the deployed project with these versions. Keep a backup of the current files first.
