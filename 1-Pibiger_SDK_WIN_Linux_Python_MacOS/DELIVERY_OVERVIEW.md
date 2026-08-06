# SAVVYCANFD — Delivery Overview

SAVVYCANFD is a cross-platform USB-CAN / CAN FD SDK and desktop trace
viewer. This release provides a native C library, a Qt6 GUI application,
and a Python wrapper — the same behaviour and same public API on Windows,
Linux, and macOS.

- **SDK version:** 5.0.0
- **Last updated:** 2026-08-06

---

## 1. What's in the Box

| File | Platform | Size | Purpose |
|---|---|---|---|
| `SAVVYCANFD-Windows-x64.zip`  | Windows x64           | 9.4 MB  | Windows C/C++ SDK — see Section 3 |
| `SAVVYCANFD-Linux-x64.tar.gz` | Linux x64             | 255 KB  | Linux C/C++ SDK, x64 build — see Section 4 |
| `SAVVYCANFD-Linux-arm64.zip`  | Linux ARM64           | 245 KB  | Linux C/C++ SDK, ARM64 build — see Section 4 |
| `SAVVYCANFD-Python.zip`       | Windows, Linux, macOS | 207 KB  | Python package — one archive covers all supported platforms — see Section 5 |
| `SAVVYCANFD-macOS-arm64.zip`  | macOS Apple Silicon   | 19.5 MB | macOS GUI app + C/C++ SDK, M-series Mac — see Section 6 |
| `SAVVYCANFD-macOS-x64.zip`    | macOS Intel           | 19.6 MB | macOS GUI app + C/C++ SDK, Intel Mac — see Section 6 |

All five SDK packages (Windows / Linux / macOS / Python) expose the
**same public API**. Code written on one platform recompiles unchanged on
another; Python code written with `usb_can` runs unchanged on every
supported platform.

### Extracting the archives

Three archives hold a single inner archive and need a second step:

```bash
unzip SAVVYCANFD-Linux-arm64.zip          # yields SAVVYCANFD-Linux-arm64.tar.gz
tar xzf SAVVYCANFD-Linux-arm64.tar.gz

# The macOS inner archive carries the same name as the outer one,
# so unpack the first step into its own directory.
unzip SAVVYCANFD-macOS-arm64.zip -d inner
unzip inner/SAVVYCANFD-macOS-arm64.zip
```

`SAVVYCANFD-Windows-x64.zip`, `SAVVYCANFD-Linux-x64.tar.gz` and
`SAVVYCANFD-Python.zip` extract directly.

---

## 2. Supported Platforms & Hardware

### CAN feature matrix

| Feature                     | Classic CAN 2.0        | CAN FD                                  |
|-----------------------------|------------------------|-----------------------------------------|
| Standard ID (11-bit)        | ✅                     | ✅                                      |
| Extended ID (29-bit)        | ✅                     | ✅                                      |
| Remote frames               | ✅                     | —                                       |
| Arbitration bitrate         | 5 kbps – 1 Mbps        | 5 kbps – 1 Mbps                         |
| Data-phase bitrate          | —                      | up to 5 Mbps (hardware-dependent)       |
| Listen-only mode            | ✅                     | ✅                                      |
| One-shot transmit           | ✅                     | ✅                                      |
| Auto-restart from bus-off   | ✅                     | ✅                                      |
| Software acceptance filter  | ✅                     | ✅                                      |

Device capabilities are reported per-adapter at runtime so applications
can adapt automatically.

### Supported adapter families

| Family                       | Windows | Linux | macOS |
|------------------------------|:-------:|:-----:|:-----:|
| PCAN-USB / PCAN-USB FD       |   ✅    |   —   |   —   |
| Standard USB-CAN adapters    |   ✅    |   ✅  |   ✅  |
| Native Linux CAN interfaces  |   —     |   ✅  |   —   |

The SDK selects the right hardware path automatically. Application code
does not change with the adapter.

### Verified Linux ARM64 hardware

| OS                        | Board                       |
|---------------------------|-----------------------------|
| Ubuntu 22.04 LTS          | NVIDIA Jetson Orin Nano     |
| Raspberry Pi OS Bookworm  | Raspberry Pi 5              |

---

## 3. Windows Package

### 3.1 Audience & requirements

- **Windows 10 (build 1809+) or Windows 11**, x64
- No prerequisites — Qt6, Visual C++ runtime, and USB runtime are all bundled
- Truly out-of-the-box

### 3.2 Folder layout

```
SAVVYCANFD-Windows-x64/
├── README.md                       Getting-started guide
├── run_SAVVYCANFD.bat              Launch the GUI (double-click)
├── bin/                            Self-contained runtime (~21 MB)
│   ├── SAVVYCANFD.exe              GUI trace viewer
│   ├── can_example.exe             CLI sample
│   ├── usb_can.dll                 SDK library
│   └── (Qt6 + support runtimes)
├── lib/usb_can.lib                 Import library
├── include/can/                    Public API headers
├── examples/basic_can.c            Sample source
├── CMakeLists.txt                  Minimal CMake project for the sample
└── third_party_license/            Bundled license notices
```

### 3.3 Quick Start

1. Extract `SAVVYCANFD-Windows-x64.zip` to any directory.
2. Plug in the USB-CAN adapter.
3. For PCAN-USB adapters, install the vendor driver per the manufacturer's
   instructions. Other USB-CAN adapters are recognised by Windows
   out-of-the-box.
4. Double-click `run_SAVVYCANFD.bat`. The GUI launches and the adapter
   appears in the device list.

### 3.4 Application development

```cpp
#include <can/usb_can_sdk.h>

// MSVC project settings
//   Additional Include Directories: SAVVYCANFD-Windows-x64\include
//   Additional Library Directories: SAVVYCANFD-Windows-x64\lib
//   Additional Dependencies:        usb_can.lib
// At runtime, put SAVVYCANFD-Windows-x64\bin on PATH,
// or copy its contents next to your .exe.
```

See `include/can/*.h` for the public API.

---

## 4. Linux Package

### 4.1 Audience & requirements

- **Ubuntu 22.04 LTS or newer** (Debian 12+, Raspberry Pi OS Bookworm)
- **Both x86_64 and ARM64** (Raspberry Pi 5, NVIDIA Jetson, Rockchip SBCs, etc.)
- System packages: `libusb-1.0-0`, `libqt6widgets6` (one apt command)

### 4.2 Folder layout

```
SAVVYCANFD-Linux-<arch>/
├── README_LINUX.md                 Getting-started + permission setup
├── lib/libusb_can.so*              SDK library (with SONAME chain)
├── bin/
│   ├── SAVVYCANFD                  GUI trace viewer
│   └── can_example                 CLI sample
├── include/can/*.h                 Public API headers (same as Windows)
├── examples/basic_can.c            Sample source
└── run_SAVVYCANFD.sh               Launch script
```

### 4.3 Quick Start

```bash
# x64 — extracts directly:
tar xzf SAVVYCANFD-Linux-x64.tar.gz
cd SAVVYCANFD-Linux-x64

# ARM64 — unzip first, then extract the tarball inside:
#   unzip SAVVYCANFD-Linux-arm64.zip
#   tar xzf SAVVYCANFD-Linux-arm64.tar.gz
#   cd SAVVYCANFD-Linux-arm64

# Install runtime dependencies (one-time)
sudo apt update
sudo apt install -y libusb-1.0-0 libqt6widgets6

# Set up USB device permission (one-time)
# See README_LINUX.md for the exact steps.

./run_SAVVYCANFD.sh
```

### 4.4 Application development

```bash
# From inside the extracted SAVVYCANFD-Linux-<arch>/ directory:
gcc my_app.c \
    -Iinclude \
    -Llib -lusb_can \
    -Wl,-rpath,'$ORIGIN/lib' \
    -o my_app
```

`-Wl,-rpath,'$ORIGIN/lib'` lets the binary find `libusb_can.so` next to
itself, so you can ship `my_app` together with the `lib/` folder.

---

## 5. Python Package

### 5.1 Audience & requirements

- **Python 3.8 – 3.12** (CPython) on Windows x64, Linux x64, Linux ARM64,
  macOS Apple Silicon, or macOS Intel
- Test automation, ECU diagnostics scripting, data logging, Jupyter notebooks
- Rapid prototyping with the same behaviour as the C/C++ packages
- Zero required Python dependencies

A single archive covers all five platforms — no per-platform install
variants. On Linux and macOS the system `libusb-1.0` is still required
(`sudo apt install -y libusb-1.0-0`, or `brew install libusb`).

### 5.2 Folder layout

```
SAVVYCANFD-Python/
├── README.md                       Detailed Python guide
├── pyproject.toml                  Standard metadata (pip install -e . works)
├── install_deps.bat / .sh          Optional dependency installer
├── run_basic_capture.bat / .sh     Smoke test — open device, send a frame
├── run_recv_loop.bat / .sh         Continuous receive loop
├── usb_can/                        The package
│   ├── __init__.py                 High-level Device class + helpers
│   └── _libs/                      Bundled native libs (auto-selected)
├── examples/
│   ├── basic_capture.py
│   └── recv_loop.py
└── tests/test_smoke.py
```

### 5.3 Quick Start

**Windows:**

```bat
:: Extract SAVVYCANFD-Python.zip, then in a command prompt:
install_deps.bat
run_basic_capture.bat
run_recv_loop.bat
```

**Linux:**

```bash
# Prerequisites are the same as the C/C++ Linux package —
# libusb-1.0-0 + the udev permission step from README_LINUX.md.

unzip SAVVYCANFD-Python.zip
cd SAVVYCANFD-Python
chmod +x *.sh
./install_deps.sh
./run_basic_capture.sh
./run_recv_loop.sh
```

### 5.4 Application usage

```python
import usb_can

# Discover adapters
for d in usb_can.discover():
    print(d.name, d.serial)

# Open, configure, send, receive
with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000)
    dev.start()

    dev.send(can_id=0x123, data=b'\x11\x22\x33\x44')

    for msg in dev.receive(timeout_ms=1000):
        print(f"{msg.id:08X}  {msg.data.hex()}  ts={msg.timestamp_us}")

    print(dev.stats())
```

CAN FD example:

```python
with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000, data_bitrate=2_000_000,
                  flags=usb_can.CAN_CAP_CANFD)
    dev.start()
    dev.send(can_id=0x123, data=bytes(range(64)),
             flags=usb_can.CAN_FLAG_FD | usb_can.CAN_FLAG_BRS)
```

### 5.5 Optional dependencies

| Feature                       | Package                | Install                              |
|-------------------------------|------------------------|--------------------------------------|
| Core (always works)           | —                      | (nothing)                            |
| Test runner                   | `pytest`               | `pip install pytest`                 |
| Notebook / plotting workflows | `numpy`, `matplotlib`  | `pip install numpy matplotlib`       |

Or run `install_deps.bat` / `install_deps.sh` for an interactive prompt.

---

## 6. macOS Package

### 6.1 Audience

End users on macOS who want SAVVYCANFD as a desktop GUI for CAN / CAN FD
trace, transmit, and DBC decoding — and developers integrating the SDK
into their own macOS application. The package covers both: the GUI app
plus a standalone dylib, the public headers, and the CLI sample, in the
same layout as the Linux packages.

### 6.2 What's in the archive

| Archive                       | Mac hardware                      |
|-------------------------------|-----------------------------------|
| `SAVVYCANFD-macOS-arm64.zip`  | Apple Silicon (M1 / M2 / M3 / M4) |
| `SAVVYCANFD-macOS-x64.zip`    | Intel Mac                         |

Pick the archive that matches your Mac's chip (Apple menu → About This
Mac → Chip). Apple Silicon Macs cannot run the Intel build, and vice
versa.

```
SAVVYCANFD-macOS-<arch>/
├── SAVVYCANFD.app                  GUI trace viewer
├── lib/libusb_can.5.0.0.dylib      SDK library (with version symlinks)
├── bin/can_example                 CLI sample
├── include/can/*.h                 Public API headers (same as Windows / Linux)
├── examples/basic_can.c            Sample source
└── run_SAVVYCANFD.sh               Launch script
```

Extract (two steps — see Section 1), then drag `SAVVYCANFD.app` to
`/Applications/`.

### 6.3 Application development

```bash
# From inside the extracted SAVVYCANFD-macOS-<arch>/ directory:
clang my_app.c \
    -Iinclude \
    -Llib -lusb_can \
    -Wl,-rpath,@executable_path/lib \
    -o my_app
```

`libusb-1.0` must be present on the target machine
(`brew install libusb`). See `DLL_USAGE.md` for deployment details.

### 6.4 First launch (Gatekeeper)

The app is unsigned. macOS will refuse the first launch with an
"unable to verify" or "damaged" prompt. Run this once in Terminal, then
double-click the app normally:

```bash
sudo xattr -dr com.apple.quarantine /Applications/SAVVYCANFD.app
```

macOS 14 (Sonoma) and earlier also support the Finder → right-click →
**Open** dialog. macOS 15 (Sequoia) requires the `xattr` command above.

### 6.5 Hardware

Plug in a supported USB-CAN adapter and launch the app. No driver
install is required.

---

## 7. Cross-Platform Quick Reference

| Aspect          | Windows C/C++                  | Linux C/C++                     | macOS C/C++                     | Python                                   |
|-----------------|--------------------------------|---------------------------------|---------------------------------|------------------------------------------|
| Package         | `SAVVYCANFD-Windows-x64.zip`   | `SAVVYCANFD-Linux-x64.tar.gz` / `-arm64.zip` | `SAVVYCANFD-macOS-<arch>.zip`  | `SAVVYCANFD-Python.zip`                  |
| GUI viewer      | `bin\SAVVYCANFD.exe`           | `bin/SAVVYCANFD`                | `SAVVYCANFD.app`                | (C/C++ GUI — Python package is headless) |
| CLI sample      | `bin\can_example.exe`          | `bin/can_example`               | `bin/can_example`               | `examples\basic_capture.py`              |
| Public API      | Same headers `include/can/*.h` | Same headers `include/can/*.h`  | Same headers `include/can/*.h`  | `import usb_can`                         |
| Launch script   | `run_SAVVYCANFD.bat`           | `run_SAVVYCANFD.sh`             | `run_SAVVYCANFD.sh`             | `run_basic_capture.bat / .sh`            |
| Qt6 runtime     | Bundled                        | System `libqt6widgets6`         | Bundled in the `.app`           | Not used                                 |
| Architectures   | x64                            | x64 + ARM64                     | Apple Silicon + Intel           | all five (single package)                |
| Package size    | 21 MB (zip 9.4 MB)             | ~660 KB per arch (~250 KB packed) | ~20 MB per arch               | 524 KB (zip 207 KB)                      |
| Supported OS    | Windows 10 / 11 x64            | Ubuntu 22.04+ / Debian 12+ / Pi OS Bookworm | macOS 12+           | All of the above + Python 3.8 – 3.12     |

The public API is identical across all SDK packages — source code
written for one recompiles unchanged on another.

---

## 8. Compatibility Matrix

| Item                                | Value                                                    |
|-------------------------------------|----------------------------------------------------------|
| SDK version                         | 5.0.0                                                    |
| CAN standards                       | CAN 2.0A/B, ISO 11898-1; CAN FD (ISO and non-ISO)        |
| Linux glibc requirement             | 2.35 or newer (Ubuntu 22.04+)                            |
| Windows requirement                 | Windows 10 build 1809 or newer; all Windows 11 versions  |
| macOS requirement                   | macOS 12 or newer                                        |
| Qt                                  | 6.x (bundled on Windows/macOS; system on Linux)          |
| Recommended C / C++ compiler        | MSVC 2022 (Windows) / GCC 11+ (Linux)                    |
| Python                              | 3.8 – 3.12, CPython                                      |
| Required Python packages            | none                                                     |
| Optional Python packages            | `numpy`, `matplotlib`, `pytest`                          |

---

## 9. Delivery Notes

1. **Cloud share or email** — send the `.zip` / `.tar.gz` directly.
2. **USB stick or air-gapped sites** — copy the archive as-is.
3. **Custom enterprise deployment** — the package layout is suitable as a
   base for re-branding (logo, signing, license-key gating).
4. **Choosing a package**
   - System integrators / desktop apps → `SAVVYCANFD-Windows-x64.zip`,
     `SAVVYCANFD-Linux-x64.tar.gz` / `SAVVYCANFD-Linux-arm64.zip`,
     `SAVVYCANFD-macOS-<arch>.zip`
   - Test automation, data logging, scripting → `SAVVYCANFD-Python.zip`
     (single archive covers all five platforms)
   - macOS end users → `SAVVYCANFD-macOS-<arch>.zip`
   - The packages are **non-exclusive** — same behaviour, different
     interface. A customer can deploy any combination.

For technical support, contact the SDK provider.
