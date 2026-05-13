# USB-CAN SDK — Delivery Overview

USB-CAN / CAN FD SDK with cross-platform binaries, GUI trace viewer, and
reference examples.

- **SDK version:** 5.0.0
- **Last updated:** 2026-05-13

---

## 1. What's in the Box

| File | Platform | Size | Purpose |
|---|---|---|---|
| `V5-SDK-DLL-CUS.zip` | Windows x64 | 19 MB | Compressed Windows C/C++ package — distribute by email or cloud share |
| `V5-SDK-DLL-CUS/` | Windows x64 | 45 MB | Extracted folder, ready to use |
| `V5-SDK-SO-CUS.tar.gz` | Linux x64 / ARM64 | 494 KB | Compressed Linux C/C++ package |
| `V5-SDK-SO-CUS/` | Linux x64 / ARM64 | 1.3 MB | Extracted folder, ready to use |
| `V5-SDK-PYTHON-CUS.zip` | Windows + Linux (x64 / ARM64) | 153 KB | Compressed Python package — bundles native libraries for all 3 platforms |
| `V5-SDK-PYTHON-CUS/` | Windows + Linux (x64 / ARM64) | 390 KB | Extracted folder, ready to use |

All three packages share the same SDK source tree and the same underlying
shared library. Code written against the C API on Windows will compile and
run unchanged on Linux; Python code written with `usb_can` runs unchanged
on every supported platform.

---

## 2. Supported Hardware

The SDK auto-selects a backend at runtime based on what is plugged in. The
public C / Python API is identical regardless of which backend is active.

| Backend | Platform | Hardware | Status |
|---|---|---|---|
| PCAN-compatible (vendor runtime DLL) | Windows | PCAN-USB / PCAN-USB FD class adapters | ✅ Production |
| libusb + gs_usb protocol | Windows | candleLight-compatible USB-CAN adapters | ✅ Production |
| libusb + gs_usb protocol | Linux | candleLight-compatible USB-CAN adapters | ✅ Production |
| SocketCAN | Linux | Any kernel-supported CAN interface (`can0`, `vcan0`, USB→SocketCAN, PCIe CAN, etc.) | ✅ Production |

### CAN feature matrix

| Feature | Classic CAN 2.0 | CAN FD |
|---|---|---|
| Standard ID (11-bit) | ✅ | ✅ |
| Extended ID (29-bit) | ✅ | ✅ |
| Remote frames | ✅ | — |
| Arbitration bitrate | 5 kbps – 1 Mbps | 5 kbps – 1 Mbps |
| Data-phase bitrate | — | up to 5 Mbps (hardware-dependent) |
| Listen-only mode | ✅ | ✅ |
| One-shot transmit | ✅ | ✅ |
| Auto-restart from bus-off | ✅ | ✅ |
| Software acceptance filter | ✅ | ✅ |

Capability flags (`CAN_CAP_*`) are reported per-device so applications can
adapt at runtime — see `can_get_device_info()`.

---

## 3. Windows Package (`V5-SDK-DLL-CUS`)

### 3.1 Target Audience

- **Windows 10 / 11 x64** users
- No prerequisites required — Qt6, Visual C++ runtime, and libusb are all bundled
- Truly out-of-the-box

### 3.2 Folder Layout

```
V5-SDK-DLL-CUS/
├── README.md                       SDK overview
├── run_viewer.bat                  Launch the GUI trace viewer (double-click)
├── bin/                            All runtime files (~45 MB, self-contained)
│   ├── canviewer.exe               GUI trace viewer
│   ├── can_example.exe             CLI capture demo
│   ├── usb_can.dll                 SDK library
│   ├── libusb-1.0.dll              USB transport (for candleLight / gs_usb adapters)
│   ├── Qt6Core.dll, Qt6Gui.dll, Qt6Widgets.dll, Qt6Svg.dll   Qt6 framework
│   ├── opengl32sw.dll, D3Dcompiler_47.dll                    Graphics stack
│   ├── platforms/qwindows.dll                                Qt platform plugin
│   └── styles/, imageformats/, iconengines/                  UI assets
├── lib/usb_can.lib                 Import library (link your application)
├── include/can/                    Public API headers
│   ├── usb_can_sdk.h               Core SDK + send / receive
│   ├── can_device.h                Device discovery and configuration
│   └── can_types.h                 Common types, status codes, capability flags
├── examples/
│   └── basic_can.c                 CLI sample source (compilable reference)
├── CMakeLists.txt                  Minimal CMake project for the example
└── third_party_license/            Bundled third-party license notices
```

### 3.3 Quick Start (End User)

```
1. Extract V5-SDK-DLL-CUS.zip to any directory (e.g., D:\usbcan\)
2. Plug in the USB-CAN adapter
3. (For PCAN-compatible adapters) install the vendor driver per the
   manufacturer's instructions
   (For candleLight / gs_usb adapters) Windows recognizes the device
   out-of-the-box — no driver install needed
4. Double-click D:\usbcan\V5-SDK-DLL-CUS\run_viewer.bat
   → GUI launches and your adapter appears in the device list
```

### 3.4 Application Development

```cpp
// Header
#include <can/usb_can_sdk.h>

// MSVC project settings:
//   Additional Include Directories:  V5-SDK-DLL-CUS\include
//   Additional Library Directories:  V5-SDK-DLL-CUS\lib
//   Additional Dependencies:         usb_can.lib
// At runtime, ensure V5-SDK-DLL-CUS\bin is on PATH, or copy the
// contents of bin\ to your executable's directory.
```

---

## 4. Linux Package (`V5-SDK-SO-CUS`)

### 4.1 Target Audience

- **Ubuntu 22.04 LTS or newer** (Debian 12+, Raspberry Pi OS Bookworm)
- **Both x86_64 and ARM64** (Raspberry Pi 5, NVIDIA Jetson, Rockchip SBCs, etc.)
- System packages required: `libusb-1.0-0`, `libqt6widgets6` (one apt command)

**Verified ARM64 platforms** (same `ubuntu22.04-arm64/` binary, no recompile):

| OS | Hardware | Status |
|---|---|---|
| Ubuntu 22.04 LTS | NVIDIA Jetson Orin Nano | ✅ |
| Raspberry Pi OS Bookworm | Raspberry Pi 5 | ✅ |

### 4.2 Folder Layout

```
V5-SDK-SO-CUS/
├── README_LINUX.md                 SDK overview and deployment guide
├── ubuntu22.04-x64/                Intel/AMD 64-bit
│   ├── lib/
│   │   ├── libusb_can.so           ← link target
│   │   ├── libusb_can.so.5         ← SONAME
│   │   └── libusb_can.so.5.0.0     ← actual library
│   ├── bin/
│   │   ├── canviewer               GUI trace viewer
│   │   └── can_example             CLI capture demo
│   ├── include/can/*.h             Public API headers (same set as Windows)
│   ├── examples/basic_can.c        Sample source
│   └── run_viewer.sh               Launch script
└── ubuntu22.04-arm64/              ARM64 (Pi 5 / Jetson / Rockchip)
    └── (same layout, ARM aarch64 binaries)
```

### 4.3 Quick Start (End User)

```bash
# 1. Extract
tar xzf V5-SDK-SO-CUS.tar.gz
cd V5-SDK-SO-CUS

# 2. Install runtime dependencies (one-time)
sudo apt update
sudo apt install -y libusb-1.0-0 libqt6widgets6

# 3a. For SocketCAN devices (kernel-supported CAN interfaces)
sudo ip link set can0 up type can bitrate 500000

# 3b. For candleLight / gs_usb USB adapters — non-root access via udev
sudo tee /etc/udev/rules.d/90-usbcan.rules > /dev/null <<'EOF'
SUBSYSTEM=="usb", ATTRS{idVendor}=="1d50", ATTRS{idProduct}=="606f", MODE="0666", GROUP="plugdev"
EOF
sudo udevadm control --reload-rules && sudo udevadm trigger
sudo usermod -aG plugdev $USER
# Log out and back in for the group change to take effect

# 4. Pick the right architecture and launch the GUI
case "$(uname -m)" in
    x86_64)  cd ubuntu22.04-x64 ;;
    aarch64) cd ubuntu22.04-arm64 ;;
esac
./run_viewer.sh
```

> **Note**: The udev rule above grants user access without claiming
> exclusive ownership of the device. Other gs_usb-aware software
> (e.g. candleLight) continues to work alongside this SDK on the same
> adapter.

### 4.4 Application Development

```bash
ARCH_DIR=ubuntu22.04-x64    # or ubuntu22.04-arm64

gcc my_app.c \
    -I$ARCH_DIR/include \
    -L$ARCH_DIR/lib -lusb_can \
    -Wl,-rpath,'$ORIGIN/lib' \
    -o my_app
```

The `-Wl,-rpath,'$ORIGIN/lib'` flag lets the resulting binary find
`libusb_can.so` next to itself at runtime, so you can ship `my_app`
together with the `lib/` folder.

---

## 5. Python Package (`V5-SDK-PYTHON-CUS`)

### 5.1 Target Audience

- **Python 3.8+** users on Windows x64, Linux x64, or Linux ARM64
- Test automation, ECU diagnostics scripts, data-logging, Jupyter notebooks
- Rapid prototyping that needs the same SDK behavior as the C/C++ packages

This package wraps the **same** `usb_can` shared library that the C/C++
packages use. There is no separate codepath: a fix to the C SDK reaches
Python users by re-bundling the same binary.

### 5.2 Folder Layout

```
V5-SDK-PYTHON-CUS/
├── README.md                       Detailed Python usage guide
├── pyproject.toml                  PEP 517 metadata (`pip install -e .` works)
├── install_deps.bat / .sh          One-click dependency installer
├── run_basic_capture.bat / .sh     Open device, send a frame, print stats
├── run_recv_loop.bat / .sh         Continuous receive loop with rate counter
├── usb_can/                        Python package
│   ├── __init__.py                 High-level `Device` class + helpers
│   ├── _raw.py                     1:1 ctypes binding (18 functions)
│   ├── _loader.py                  Cross-platform native-library locator
│   └── _libs/                      Native libraries (auto-selected by OS+arch)
│       ├── windows-x64/            usb_can.dll + libusb-1.0.dll
│       ├── linux-x64/              libusb_can.so / .so.5 / .so.5.0.0
│       └── linux-arm64/            libusb_can.so / .so.5 / .so.5.0.0
├── examples/
│   ├── basic_capture.py            Counterpart to C basic_can.c
│   └── recv_loop.py                Headless receive-rate measurement
└── tests/test_smoke.py             No-hardware load + symbol-resolution test
```

### 5.3 Quick Start (End User)

**Windows:**
```bat
:: 1. Extract V5-SDK-PYTHON-CUS.zip to any directory
:: 2. Plug in the USB-CAN adapter
:: 3. Open a command prompt in V5-SDK-PYTHON-CUS\
install_deps.bat                    :: installs optional dependencies
run_basic_capture.bat               :: smoke test
run_recv_loop.bat                   :: live receive loop
```

**Linux (Ubuntu 22.04, Debian 12+, Raspberry Pi OS Bookworm):**
```bash
# Same prerequisites as the C/C++ Linux package: libusb-1.0-0 and
# the udev rule. See Section 4.3.

unzip V5-SDK-PYTHON-CUS.zip
cd V5-SDK-PYTHON-CUS
chmod +x *.sh
./install_deps.sh
./run_basic_capture.sh
./run_recv_loop.sh
```

### 5.4 Application Development

```python
import usb_can

# Discover adapters
for d in usb_can.discover():
    print(d.name, d.driver, d.serial)
# -> "candleLight"  "LibUsbCAN"  "001A..."

# Open, configure, send, receive
with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000)        # 500 kbps classic CAN
    dev.start()

    dev.send(can_id=0x123, data=b'\x11\x22\x33\x44')

    for msg in dev.receive(timeout_ms=1000):
        print(f"{msg.id:08X}  {msg.data.hex()}  ts={msg.timestamp_us}")

    print(dev.stats())                    # {'rx': N, 'tx': N, 'errors': 0, ...}
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

For low-level needs, `usb_can._raw` exposes the full 18-function C API
exactly as declared in `include/can/*.h`.

### 5.5 Optional Dependencies

The core package has **zero required dependencies** — pure ctypes against
the bundled native library. Optional install only if you want extras:

| Feature | Package | Install |
|---|---|---|
| Core (always works) | — | (nothing) |
| Test runner | `pytest` | `pip install pytest` |
| Notebook / plotting workflows | `numpy`, `matplotlib` | `pip install numpy matplotlib` |

Or use `install_deps.bat` / `install_deps.sh` for an interactive prompt.

---

## 6. Cross-Platform Quick Reference

| Aspect | Windows C/C++ | Linux C/C++ | Python |
|---|---|---|---|
| Package | `V5-SDK-DLL-CUS` | `V5-SDK-SO-CUS` | `V5-SDK-PYTHON-CUS` |
| Main library | `bin\usb_can.dll` | `lib/libusb_can.so*` | Same `.dll` / `.so` (bundled in `_libs/<platform>/`) |
| Link / import | `lib\usb_can.lib` | Link against `.so` | `import usb_can` (ctypes, no link step) |
| GUI viewer | `bin\canviewer.exe` | `bin/canviewer` | (use C/C++ viewer; Python pkg is headless) |
| CLI sample | `bin\can_example.exe` | `bin/can_example` | `examples\basic_capture.py` |
| Sample source | `examples\basic_can.c` | Same | `examples\*.py` (2 scripts) |
| Launch script | `run_viewer.bat` | `run_viewer.sh` | `run_basic_capture.bat` / `.sh` |
| Qt6 runtime | Bundled in `bin\` | System `libqt6widgets6` | Not used |
| C runtime | Bundled in `bin\` | System `libc` | System Python interpreter |
| USB library | Bundled `bin\libusb-1.0.dll` | System `libusb-1.0-0` | Bundled in `_libs/windows-x64/`, system on Linux |
| Driver setup | Vendor driver (PCAN) / none (gs_usb) | udev rule (Section 4.3) | Same as the matching C/C++ package |
| Architectures | x64 only | x64 + ARM64 | x64 + ARM64 (single package) |
| Package size | 45 MB (zip 19 MB) | 1.3 MB (tar.gz 494 KB) | 390 KB (zip 153 KB) |
| Supported OS | Windows 10 / 11 x64 | Ubuntu 22.04+ / Debian 12+ / Raspberry Pi OS Bookworm | All of the above + Python 3.8 – 3.12 |

---

## 7. Source Compatibility Across Platforms

The `include/can/*.h` headers are **identical** in the Windows and Linux
C/C++ packages. Application code written on Windows can be recompiled on
Linux without changes, and vice versa. The Python package binds the same
18 public functions one-to-one through `usb_can._raw`, so behavior is
consistent across all three packages.

### Public API Highlights — C/C++

```c
/* Initialization */
can_status_t can_sdk_init(void);
can_status_t can_sdk_shutdown(void);

/* Device discovery */
int          can_discover(can_device_info_t *info, int max_devices);
can_status_t can_get_device_info(int index, can_device_info_t *info);

/* Open / close */
can_status_t can_open(can_handle_t *handle, int device_index);
can_status_t can_close(can_handle_t handle);

/* Configure (bitrate, CAN FD, listen-only, ...) */
can_status_t can_configure(can_handle_t handle, const can_config_t *config);
can_status_t can_get_config(can_handle_t handle, can_config_t *config);

/* Bus control */
can_status_t can_start(can_handle_t handle);
can_status_t can_stop(can_handle_t handle);
can_status_t can_reset(can_handle_t handle);

/* I/O */
can_status_t can_send   (can_handle_t handle, const can_msg_t *msg);
int          can_receive(can_handle_t handle, can_msg_t *msgs, int max_count, int timeout_ms);

/* Diagnostics */
can_status_t can_get_stats  (can_handle_t handle, can_stats_t *stats);
can_status_t can_reset_stats(can_handle_t handle);
can_status_t can_get_state  (can_handle_t handle, int *state);
```

For the full API surface, see the headers under `include/can/`.

### Public API Highlights — Python

```python
import usb_can

# Discovery
usb_can.discover()                          # list of DeviceInfo

# High-level Device class (context manager)
with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000)          # → can_configure
    dev.start()                             # → can_start
    dev.send(can_id=0x123, data=b'...')     # → can_send
    for msg in dev.receive(timeout_ms=100): # → can_receive
        ...
    print(dev.stats())                      # → can_get_stats

# Low-level 1:1 binding (escape hatch — same names as the C API)
from usb_can import _raw
_raw.can_send(handle, msg_ptr)
```

---

## 8. Compatibility Matrix

| Item | Value |
|---|---|
| SDK version | 5.0.0 |
| CAN standards | CAN 2.0A/B, ISO 11898-1; CAN FD (ISO and non-ISO) |
| USB transports | libusb-1.0 (cross-platform), WinUSB (Windows), SocketCAN (Linux kernel) |
| Linux glibc requirement | 2.35 or newer (Ubuntu 22.04+) |
| Windows requirement | Windows 10 build 1809 or newer, all Windows 11 versions |
| Qt | 6.x (bundled on Windows) / 6.2+ (system on Linux) |
| libusb | 1.0.x |
| Recommended C compiler for customers | MSVC 2022 (Windows) / GCC 11+ (Linux) |
| Recommended C++ compiler for customers | MSVC 2022 (Windows) / G++ 11+ (Linux) |
| Python version (V5-SDK-PYTHON-CUS) | 3.8 – 3.12, CPython |
| Required Python packages | none (pure ctypes) |
| Optional Python packages | `numpy`, `matplotlib`, `pytest` (test runner) |

---

## 9. Delivery Notes

1. **Cloud share or email** — send the `.zip` / `.tar.gz` archive directly
2. **USB stick or air-gapped sites** — copy the entire folder
3. **Custom enterprise deployment** — the package layout is suitable as a
   base for re-branding (logo, signing, license-key gating)
4. **Choosing a package**
   - System integrators / desktop apps → `V5-SDK-DLL-CUS` (Windows) +
     `V5-SDK-SO-CUS` (Linux)
   - Test automation, data logging, scripting → `V5-SDK-PYTHON-CUS`
     (single archive covers Win + Linux, x64 + ARM64)
   - The three packages are **non-exclusive** — same library, different
     interface. A customer can deploy any combination.

For technical support, contact the SDK provider.
