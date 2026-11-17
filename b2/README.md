# Bashir Electronic – 14.02 No-jb2 Experimental Edition

**Build date:** 2026-11-17  
**Purpose:** A separate comparison build that removes the `jb2.js` filename and routes 14.00 / 14.02 through `slopkit/jb.js`.

## What changed

- The existing 14.00 / 14.02 Afterglow runner formerly named `jb2.js` is now named `jb.js`.
- The existing Bashir loader formerly named `jb.js` is preserved as `jb_legacy_135x.js` and remains assigned to the 13.02–13.52 route.
- `index.html` routes 13.02–13.52 to `jb_legacy_135x.js`, and 14.00 / 14.02 to `jb.js`.
- `slopkit.manifest` caches both entry files and no longer lists `jb2.js`.
- The Afterglow runner's watchdog now has a terminal flag so a queued timer callback cannot show a stale retry notice after completion.
- Firmware tables, patch files, GoldHEN payload bytes, and the Afterglow execution sequence are otherwise retained from the source Stability Edition archive.

## Important comparison note

This build tests the **filename / routing layout without `jb2.js`** while preserving the project's current 14.00 / 14.02 Afterglow implementation. It is **not** a wholesale import of GamerHack's complete `jb.js` source. GamerHack's unified loader differs internally and supports a broader range in a single entry file; this package deliberately keeps Bashir's existing 13.02–13.52 loader isolated to reduce variables during comparison.

## Firmware routing

- 9.00–9.60 → `900/alert.js`
- 10.00–11.02 → `css/main.js`
- 11.50–12.02 → `slopkit/chain_lapse.js`
- 12.50–13.00 → `slopkit/chain_poops.js`
- 13.02–13.52 → `slopkit/jb_legacy_135x.js`
- 14.00 / 14.02 → `slopkit/jb.js`

## Offline cache

`slopkit.manifest` includes `slopkit/patches/1402.bin` and the GoldHEN payload. The `1402.bin` file is bundled in this ZIP. Upload the complete `b2` folder to a **separate test path** (for example, `/b2-no-jb2/`) so its AppCache manifest does not collide with your stable deployment. Clear old site data for that test path before installing the cache.

## Test checklist

1. Keep the known-good stable deployment untouched.
2. Upload the whole `b2` folder to a separate test directory.
3. Install the cache and confirm it completes.
4. Compare 14.02 startup and GoldHEN status against the stable version.
5. Separately confirm 14.00 and the 13.02–13.52 routes still resolve to their preserved entry files.
6. Do not repeatedly retry after a hard crash or power-off; record the last visible message and stop testing until the cause is understood.

## Verification limits

Static archive, manifest, resource-path, and JavaScript syntax checks can be performed on a computer. This package has **not** been tested on physical PS4 hardware. A successful cache install does not prove exploit stability.

## Upstream references

- GamerHack G2All: https://github.com/GamerHack/GamerHack.github.io/tree/main/g2all
- Afterglow: https://github.com/well0nez/afterglow-web
- Bashir project: https://github.com/pas3/8/tree/main/b2
