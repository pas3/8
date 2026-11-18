# Bashir Electronic – Bollywood Unified 13/14 Experimental Edition

**Build date:** 2026-11-17  
**Purpose:** One `jb.js` entry point for the supported 13.02–13.52 and 14.00/14.02 paths, while retaining separate firmware tables and only executing the branch selected for the detected firmware.

## What changed

- `slopkit/jb.js?v=20` is the single entry point for 13.02, 13.04, 13.50, 13.52, 14.00, and 14.02.
- The dispatcher uses the exact firmware key returned by `ps4_offsets.js`; it does not infer support merely from a numeric range.
- The previous 13.x engine and the tested 14.00/14.02 Afterglow engine are placed in isolated function scopes inside the same module. Only the matching engine is invoked.
- `jb_legacy_135x.js` and `jb2.js` are not required by this build.
- The cache manifest contains the exact versioned entry URL used by `index.html`.
- User-facing status messages use **Bollywood / بوليوود**.

## Payload identity is unchanged

“Bollywood” is a display name only. The actual payload remains `goldhen_2.4b18.14.bin`. Its filename, mode (`goldhen`), bytes, and SHA-256 are unchanged. No payload binary was renamed or modified.

## Firmware routes

- 9.00–9.60 → `900/alert.js`
- 10.00–11.02 → `css/main.js`
- 11.50–12.02 → `slopkit/chain_lapse.js`
- 12.50–13.00 → `slopkit/chain_poops.js`
- 13.02, 13.04, 13.50, 13.52 → `slopkit/jb.js?v=20` (13.x engine branch)
- 14.00, 14.02 → `slopkit/jb.js?v=20` (Afterglow 14.x engine branch)

Other values in the broad 13.02–13.52 index range are rejected if `ps4_offsets.js` has no exact entry.

## Offline cache

`slopkit.manifest` contains `slopkit/jb.js?v=20`, the common modules, `goldhen_2.4b18.14.bin`, and `slopkit/patches/1402.bin` (641 bytes). All referenced files are included in this ZIP. The obsolete separate engine files are not included.

Upload the complete `b2` folder to a **separate test path** (for example, `/b2-bollywood-unified/`). Do not overwrite the known-good deployment. Clear old site data for the test path and install its cache independently.

## Test checklist

1. Keep the currently working deployment untouched.
2. Upload the complete `b2` folder to a separate test path.
3. Install the cache and confirm it completes.
4. Test 14.02 first, then 14.00.
5. Test 13.02, 13.04, 13.50, and 13.52 individually; do not infer support for intermediate values.
6. Compare startup time, cache completion, success messages, browser reopen, and offline behavior.
7. Stop testing after a hard crash or power-off; record the last visible message instead of repeatedly retrying.

## Verification limits

The archive, manifest, resource paths, exact firmware-key lookup, and JavaScript syntax were checked on a computer. This merged build has **not** been tested on a physical PS4. Static checks do not establish activation speed, exploit reliability, or hardware stability. Keep the previously tested 14.02 build as the rollback copy.

## Upstream references

- GamerHack G2All: https://github.com/GamerHack/GamerHack.github.io/tree/main/g2all
- Afterglow: https://github.com/well0nez/afterglow-web
- Bashir project: https://github.com/pas3/8/tree/main/b2

The currently inspected GamerHack `index.html` routes 13.02–13.52 to `jb.js?v=19` and 14.00 to `jb2.js`. This package combines the two Bashir engine bodies behind one `jb.js` entry; it does not claim to copy a single-file upstream implementation.
