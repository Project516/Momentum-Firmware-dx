# AGENTS.md

A personal fork of Momentum firmware for the Flipper Zero. It tracks Momentum
and merges OFW `dev` on top, so the device gets OFW fixes before Momentum
releases them.

## Direction

- Stay close to both upstreams. Keep fork-only changes small so merges stay
  clean.
- Stay compatible with the official Flipper mobile apps (RPC over BLE and USB,
  the Apps catalog).
- Stability on a real device beats new features.

## Glossary

- **OFW**: official firmware, `flipperdevices/flipperzero-firmware`, remote
  `ofw`.
- **mntm**: Momentum upstream, `Next-Flip/Momentum-Firmware`.
- **API version**: the `Version` row in `targets/*/api_symbols.csv`. The
  mobile app sends it to the Apps catalog to pick app builds.

## Syncing OFW

Merge `ofw/dev` into `dev` with the message
`chore: merge flipperzero-firmware dev into dev`.

Keep the API version pinned to the OFW `release` value in both targets, even
when OFW `dev` or Unleashed raise it. CI fails on any other value.

## Checks

- CI runs `./fbt copro_dist updater_package fap_dist`, then fails if the build
  changed any tracked file (fbt rewrites `api_symbols.csv` on new symbols).
- `./fbt lint_all` checks formatting.
- `./fbt FIRMWARE_APP_SET=unit_tests updater_package` builds the unit test
  firmware. It runs the tests on boot and shows the result on screen.
- f18 (`TARGET_HW=18`) is not maintained in Momentum and does not build.
- If the mobile app's screen mirror is blank, check Bluetooth range before
  debugging firmware.
