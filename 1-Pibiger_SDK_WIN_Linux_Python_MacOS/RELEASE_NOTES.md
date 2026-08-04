# SAVVYCANFD SDK — Release Notes

**Version 5.0.0 · 2026-07-03**

SAVVYCANFD is a cross-platform USB-CAN / CAN FD SDK. This release ships
a native C library, a Qt6 desktop GUI, and a Python wrapper — built from
a single source tree so that C, C++, and Python code written against the
public API behaves identically across Windows, Linux, and macOS.

## Packages in this release

| Archive                            | Platform                          | Content                                                        |
|------------------------------------|-----------------------------------|----------------------------------------------------------------|
| `SAVVYCANFD-Windows-x64.zip`       | Windows 10 / 11 (x64)             | `usb_can.dll`, GUI, CLI example, headers                       |
| `SAVVYCANFD-Linux-x64.tar.gz`      | Ubuntu 22.04+ / Debian 12+ (x64)  | Shared library, GUI, CLI example, headers                      |
| `SAVVYCANFD-Linux-arm64.tar.gz`    | Ubuntu 22.04+ / Raspberry Pi OS   | Same as above, aarch64                                         |
| `SAVVYCANFD-Python.zip`            | Windows + Linux (x64 + ARM64)     | Python package with bundled native libraries for all platforms |
| `SAVVYCANFD-macOS-arm64.zip`    | macOS 12+ Apple Silicon           | `SAVVYCANFD.app` + standalone `.dylib`, headers, CLI example   |
| `SAVVYCANFD-macOS-x64.zip`      | macOS 12+ Intel                   | `SAVVYCANFD.app` + standalone `.dylib`, headers, CLI example   |

Every archive is self-contained: extract, follow the bundled README, run.
No installer required.

## Highlights

- **Unified public API across Windows, Linux, and Python.** 18 public
  functions cover discovery, configuration, bus control, transmit/receive,
  and statistics. Code written on one platform recompiles unchanged on
  another.
- **Broad USB-CAN adapter support.** PCAN-USB / PCAN-USB FD adapters and
  standard USB-CAN adapters are supported side-by-side. Adapter
  auto-selection at runtime means the application code is identical
  either way.
- **Full CAN FD feature set.** Standard and extended IDs, arbitration and
  data-phase bitrates, ISO and non-ISO framing, listen-only mode,
  one-shot transmit, auto-restart from bus-off.
- **Qt6 desktop GUI on every platform.** The `SAVVYCANFD` viewer runs on
  Windows, Linux, and macOS with the same feature set: live trace,
  transmit list, DBC decoding, and bus-load monitoring.
- **First-class Linux ARM64.** Verified on Raspberry Pi 5 and NVIDIA
  Jetson Orin Nano. Same source, same behaviour as x64.
- **Single Python archive covers every supported platform.** `usb_can`
  bundles native libraries for Windows x64, Linux x64, and Linux ARM64 —
  the same archive works on all three. Zero required Python dependencies.
- **macOS desktop app.** Dedicated `SAVVYCANFD.app` builds for both Apple
  Silicon and Intel Macs.

## Compatibility

| Item                   | Value                                                 |
|------------------------|-------------------------------------------------------|
| CAN standards          | CAN 2.0A/B (ISO 11898-1); CAN FD (ISO and non-ISO)    |
| Arbitration bitrate    | 5 kbit/s – 1 Mbit/s                                   |
| Data-phase bitrate     | up to 5 Mbit/s (adapter-dependent)                    |
| Windows                | 10 build 1809 or newer; all Windows 11 releases       |
| Linux                  | Ubuntu 22.04+, Debian 12+, Raspberry Pi OS Bookworm   |
| macOS                  | 12 Monterey and newer                                 |
| Python                 | 3.8 – 3.12, CPython                                   |

## macOS first launch

The macOS `SAVVYCANFD.app` is shipped without an Apple Developer ID
signature. On first launch macOS Gatekeeper will refuse the app with an
"unable to verify" or "damaged" prompt. Run this once in Terminal, then
double-click the app normally:

```bash
sudo xattr -dr com.apple.quarantine /Applications/SAVVYCANFD.app
```

Subsequent launches do not require the command. macOS 14 (Sonoma) and
earlier also support the Finder → right-click → **Open** dialog; macOS 15
(Sequoia) requires the `xattr` command above.

## Getting support

For integration questions, hardware compatibility, or product feedback,
contact the SDK provider through the channel used to receive this release.
