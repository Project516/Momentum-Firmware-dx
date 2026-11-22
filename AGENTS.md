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
- **momentum-dx**: this fork and its GitHub org. The website is
  `momentum-dx/v2.momentum-fw.dev`, served at
  `https://momentum-dx.project516.dev`.
- **Release tag**: `dx-YYYY.MM.DD` (`-2` for a second release the same day) on
  a commit on `dev`. The tag name is the firmware version on the device.
- **API version**: the `Version` row in `targets/*/api_symbols.csv`. The
  mobile app sends it to the Apps catalog to pick app builds.

## Syncing OFW

Merge `ofw/dev` into `dev` with the message
`chore: merge flipperzero-firmware dev into dev`.

Keep the API version pinned to the OFW `release` value in both targets, even
when OFW `dev` or Unleashed raise it. CI fails on any other value.

## Releasing

1. Test the commit on a device.
2. Tag it on `dev` and push the tag: `git tag dx-YYYY.MM.DD && git push origin dx-YYYY.MM.DD`.
3. `.github/workflows/release.yml` builds it and publishes the GitHub Release.
4. The website picks up the release within 30 minutes. It serves the latest 5
   releases and never shows dev builds.

The workflow fails if the tag is not `dx-YYYY.MM.DD[-N]` or the commit is not on
`dev`. Only `dx-*` tags make releases, so do not push `mntm-*` tags.

## Checks

- CI runs `./fbt copro_dist updater_package fap_dist`, then fails if the build
  changed any tracked file (fbt rewrites `api_symbols.csv` on new symbols).
- `./fbt lint_all` checks formatting.
- `./fbt FIRMWARE_APP_SET=unit_tests updater_package` builds the unit test
  firmware. It runs the tests on boot and shows the result on screen.
- f18 (`TARGET_HW=18`) is not maintained in Momentum and does not build.
- If the mobile app's screen mirror is blank, check Bluetooth range before
  debugging firmware.
