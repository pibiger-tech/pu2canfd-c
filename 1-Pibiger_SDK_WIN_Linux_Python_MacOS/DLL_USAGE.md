# SAVVYCANFD — Library Usage Guide

**SDK version:** 5.0.0

This guide covers how to integrate and deploy the SAVVYCANFD USB-CAN /
CAN FD SDK library (`usb_can.dll` on Windows, `libusb_can.so` on Linux,
`libusb_can.dylib` on macOS) in your own application. If you only need
the Python interface, jump to [Section 5](#5-python-38).

---

## 1. Where the library lives in each package

| Package | Library file | Import library / header |
|---|---|---|
| `SAVVYCANFD-Windows-x64.zip`    | `bin/usb_can.dll` (+ `bin/libusb-1.0.dll`) | `lib/usb_can.lib`, `include/can/*.h` |
| `SAVVYCANFD-Linux-x64.tar.gz`   | `lib/libusb_can.so.5.0.0` (+ SONAME symlinks) | `include/can/*.h` |
| `SAVVYCANFD-Linux-arm64.tar.gz` | Same layout as x64 | Same |
| `SAVVYCANFD-macOS-arm64.tar.gz` | `SAVVYCANFD.app/Contents/Frameworks/libusb_can.5.0.0.dylib` | `include/can/*.h` |
| `SAVVYCANFD-macOS-x64.tar.gz`   | Same layout as arm64 | Same |
| `SAVVYCANFD-Python.zip`         | Native libraries for Windows x64 / Linux x64 / Linux ARM64 bundled inside | Not required — Python wraps them |

The three source-integration packages (Windows / Linux) expose the same
public C API through the same three headers under `include/can/`.

---

## 2. C / C++ integration

### Include and link

```c
#include <can/usb_can_sdk.h>
```

| Platform | Link flag |
|---|---|
| Windows (MSVC)      | `usb_can.lib` |
| Linux (GCC / Clang) | `-lusb_can`   |
| macOS (Clang)       | `-lusb_can`   |

Minimum runtime dependency: **libusb 1.0**.
- Windows: ship `libusb-1.0.dll` next to your application executable.
  The file is included in `SAVVYCANFD-Windows-x64/bin/`.
- Linux: install `libusb-1.0-0` via your distro package manager
  (`sudo apt install -y libusb-1.0-0`).
- macOS: install via Homebrew (`brew install libusb`) or bundle it
  inside your `.app`.

### Minimum example

```c
#include <can/usb_can_sdk.h>
#include <stdio.h>
#include <string.h>

int main(void) {
    can_sdk_init();

    can_device_info_t devs[CAN_MAX_DEVICES];
    int n = can_discover(devs, CAN_MAX_DEVICES);
    if (n <= 0) { can_sdk_shutdown(); return 1; }

    can_handle_t h = NULL;
    can_open(&h, 0);

    can_config_t cfg;
    memset(&cfg, 0, sizeof(cfg));
    cfg.bitrate = 500000;
    cfg.sample_point = 875;
    can_configure(h, &cfg);
    can_start(h);

    can_msg_t tx;
    memset(&tx, 0, sizeof(tx));
    tx.id  = 0x123;
    tx.dlc = 8;
    for (int i = 0; i < 8; i++) tx.data[i] = (uint8_t)(i + 1);
    can_send(h, &tx);

    can_msg_t rx[16];
    int rxn = can_receive(h, rx, 16, 2000);
    printf("Received %d frame(s)\n", rxn);

    can_stop(h);
    can_close(h);
    can_sdk_shutdown();
    return 0;
}
```

The full working sample is `examples/basic_can.c` inside each SDK
package, and each Windows / Linux package ships a minimal
`CMakeLists.txt` at the top level that builds it against the bundled
headers and library.

### Public API headers

| Header             | Contents                                        |
|--------------------|-------------------------------------------------|
| `usb_can_sdk.h`    | Single-include entry point                      |
| `can_types.h`      | Types, flags, status codes, message struct      |
| `can_device.h`     | Device-control API declarations                 |

---

## 3. Runtime deployment

When shipping your compiled application to a target machine, copy the
following files. You do **not** need the SDK's `include/`, `lib/`, or
`examples/` at runtime.

### Windows

Copy alongside your `.exe`:

```
usb_can.dll
libusb-1.0.dll
```

If you also ship the GUI viewer, copy the full contents of
`SAVVYCANFD-Windows-x64/bin/` (Qt6 runtime included).

### Linux (x64 or ARM64)

Install to your app's rpath or a system location such as
`/usr/local/lib/`:

```
libusb_can.so.5.0.0
libusb_can.so.5     (symlink to libusb_can.so.5.0.0)
libusb_can.so       (symlink)
```

Run `sudo ldconfig` after installing to `/usr/local/lib/`.
`libusb-1.0` must be provided by the distro (`libusb-1.0-0`).

The recommended pattern for a self-contained deployment is to ship
`my_app` and a sibling `lib/` folder, then compile with
`-Wl,-rpath,'$ORIGIN/lib'` so the binary finds `libusb_can.so` next to
itself without polluting `/usr/lib`.

### macOS

The SDK dylib lives inside the app bundle at
`SAVVYCANFD.app/Contents/Frameworks/libusb_can.5.0.0.dylib`. To link
your own binary against it:

```bash
APP=SAVVYCANFD.app
FRAMEWORKS=$APP/Contents/Frameworks

clang my_app.c \
    -I SAVVYCANFD-macOS-arm64/include \
    -L $FRAMEWORKS -lusb_can \
    -Wl,-rpath,@executable_path/$FRAMEWORKS \
    -o my_app
```

Ship `my_app` together with the `SAVVYCANFD.app` bundle so the rpath
resolves at runtime.

---

## 4. Overriding where the library is loaded from

For the Python package the library search order is:

1. `USB_CAN_LIB` environment variable (full path to the shared library)
2. Bundled `usb_can/_libs/<platform>/`
3. Sibling files in the package directory
4. The system loader search path

```bash
# Linux / macOS
export USB_CAN_LIB=/path/to/libusb_can.so
python examples/basic_capture.py

# Windows
set USB_CAN_LIB=C:\path\to\usb_can.dll
python examples\basic_capture.py
```

For C / C++ applications, the loader uses the standard OS search path
(`PATH` on Windows, `LD_LIBRARY_PATH` on Linux, `DYLD_LIBRARY_PATH` /
rpath on macOS).

---

## 5. Python (3.8+)

The Python package bundles the native library for Windows x64, Linux
x64, and Linux ARM64. No separate C library install is required.

```bash
unzip SAVVYCANFD-Python.zip
cd SAVVYCANFD-Python
./install_deps.sh          # optional — no required external deps
./run_basic_capture.sh
```

```python
import usb_can

with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000)
    dev.start()
    dev.send(can_id=0x123, data=bytes(range(8)))
    for msg in dev.receive(timeout_ms=1000):
        print(f"{msg.id:08X}  {msg.data.hex()}")
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

Full API reference and the standalone package layout are documented in
`SAVVYCANFD-Python/README.md` inside the archive.

---

## 6. Binary compatibility

The library preserves ABI within the 5.x line. Linux SONAME
`libusb_can.so.5` and macOS current-version `5` do not change across
minor releases, so an application compiled against 5.0.x runs against
a later 5.x drop-in without recompilation — replace the shared library
file in place and restart the application.

Windows uses a fixed `usb_can.dll` file name and the same `usb_can.lib`
import library across the 5.x line.

---

## 7. Where to look next

- `RELEASE_NOTES.md` — this release's new features and supported
  platforms.
- `DELIVERY_OVERVIEW.md` — full package inventory and per-platform
  installation walkthrough.
- Each package's top-level `README*.md` — per-package quick start and
  troubleshooting.
