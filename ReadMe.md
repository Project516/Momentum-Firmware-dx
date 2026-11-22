<p align="center"><img src=".github/assets/mdx_wordmark.png" alt="Momentum-dx" width="300"></p>

# Momentum-dx

A bleeding-edge fork of Momentum Firmware for the Flipper Zero.

Momentum-dx is an unofficial fork. It is not affiliated with Next-Flip or the Momentum team.

Website and web updater: https://momentum-dx.project516.dev

## What it adds over Momentum

- OFW `dev` is merged on top of Momentum, so the device gets official firmware fixes before Momentum releases them.
- Changes from Unleashed are merged in.
- The bundled apps come from the [momentum-dx fork of Momentum-Apps](https://github.com/momentum-dx/Momentum-Apps). They include Specter, NFC Tools and BarCode Scanner Emulator.
- The API version stays pinned to the OFW `release` value. The official Flipper mobile apps and the Apps catalog keep working.

Everything else is Momentum: Momentum Settings, Asset Packs, Bad-KB and the rest. See the [Momentum README](https://github.com/Next-Flip/Momentum-Firmware#readme) for those features.

## Install

Web updater (Chrome or Edge):

1. Close qFlipper.
2. Open https://momentum-dx.project516.dev/update.
3. Click Connect, select your Flipper, then click Install.

From a release file:

1. Download `flipper-z-f7-update-<tag>.tgz` from the [latest release](https://github.com/momentum-dx/Momentum-Firmware-dx/releases/latest).
2. Open [qFlipper](https://flipperzero.one/update), connect your Flipper and click Install from file.
3. Select the `.tgz` and wait for the update to finish.

The Flipper mobile app can also install the downloaded `.tgz`.

## Releases

A release is a tested commit on `dev` with a tag named `dx-YYYY.MM.DD`. A second release on the same day is `dx-YYYY.MM.DD-2`. CI builds the tag and publishes a GitHub Release with the update `.tgz`, the full `.dfu` and the SDK `.zip`.

The website lists the latest 5 releases and serves their files. It updates within 30 minutes of a release. Builds from `dev` are not published. Build from source to run one.

## Build

```bash
git clone --recursive https://github.com/momentum-dx/Momentum-Firmware-dx.git
cd Momentum-Firmware-dx

# Flash over USB, with qFlipper closed
./fbt flash_usb_full

# Build the update package
./fbt updater_package
```

## Credits

- [Momentum Firmware](https://github.com/Next-Flip/Momentum-Firmware) by Next-Flip and the Momentum team. This fork is based on their work.
- [Official Flipper Zero firmware](https://github.com/flipperdevices/flipperzero-firmware) by Flipper Devices.
- [Unleashed firmware](https://github.com/DarkFlippers/unleashed-firmware) by DarkFlippers.

Momentum-dx is licensed under the GNU General Public License v3.0. See [LICENSE](LICENSE).
