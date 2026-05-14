# PIBIGER SavvyCAN-FD Series

**Professional USB-CAN FD Interface with CANVIEWER & SDK**

![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue) ![Standard](https://img.shields.io/badge/Standard-SocketCAN%20%7C%20CAN%20FD-blue)

---

## Overview

**PIBIGER SavvyCAN-FD Series** provides professional-grade USB interfaces for CAN/CAN FD bus communication. The series includes single-channel and dual-channel models designed for different application requirements. All models provide:

- **SAVVYCANFD GUI** — A powerful GUI application for real-time CAN bus monitoring, analysis, and debugging
- **SAVVYCANFD-SDK** — A cross-platform C/C++ and Python API for custom application development
- **SocketCAN Support** — Full Linux SocketCAN integration
- **CAN FD Compliance** — Support for high-speed CAN FD communication (up to 12 Mbit/s)

---

## Key Features

- **SocketCAN Compatible** — Fully compatible SocketCAN devices for Linux systems
- **SavvyCAN Support** — Official SavvyCAN software support for CAN FD communication
- **Third-Party Compatibility** — Compatible with Busmaster, SocketCAN, and other standard tools
- **High-Speed Data Transfer** — Supports CAN FD bit rates from 25 kbit/s up to 12 Mbit/s maximum
- **Precision Timing** — Timestamp resolution up to 1 microsecond for accurate timing analysis
- **Robust Isolation** — Each CAN FD signal and power line separately isolated against USB up to 2.5 kV
- **Cross-Platform** — Windows, Linux, and macOS support

---

## Hardware Specifications

### Common Specifications (All Models)

| Specification | Details |
| :--- | :--- |
| **CAN Standard** | CAN 2.0B / CAN FD |
| **Arbitration Bitrate** | 25 kbit/s to 1 Mbit/s |
| **Data Bitrate (FD)** | Up to 12 Mbit/s |
| **Timestamp Resolution** | 1 microsecond |
| **Galvanic Isolation** | 2.5 kV per channel (signal and power) |
| **Operating Temperature** | 0°C to 50°C |
| **Power Supply** | USB bus powered (5V) |
| **USB Protocol** | USB 2.0 High-Speed (480 Mbps) |
| **Compliance** | CE, FCC certified |

### Product Models

| Model | Channels | Connectors | Applications | Product Link |
| :--- | :--- | :--- | :--- | :--- |
| **SavvyCAN-FD-C** | 1 × CAN/CAN FD | USB Type-A, 1 × CAN D-Sub 9-pin | Single CAN network monitoring, automotive diagnostics | [View Product](https://www.pibiger-tech.com/product/savvycan-fd-c/) |
| **SavvyCAN-FD-X2** | 2 × CAN/CAN FD (independent) | USB Type-A, 2 × CAN D-Sub 9-pin | Multi-network monitoring, CAN gateway, network bridging | [View Product](https://www.pibiger-tech.com/product/savvycan-fd-x2/) |

---

## Documentation

- **[Hardware Manual](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd#id-2-hardware-manual)** — Detailed hardware specifications and pinouts
- **[Quick Start Guide](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/quick-start-guide)** — Step-by-step instructions to get your device running
- **[CAN FD Protocol](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/can-fd-protocal)** — Information on CAN FD standard and data rates

---

## Repository Contents

| Directory / File | Platform | Description |
| :--- | :--- | :--- |
| `0-Win_Driver/` | Windows | Windows driver download link |
| `1-Pibiger_SDK_WIN_Linux_Python/` | Windows / Linux / Python | Pibiger SDK packages (see below) |
| `2-MacOS_SDK/` | macOS | macOS SDK package |
| `3_Linux_Soft_SocketCAN/` | Linux | SocketCAN C examples, can-utils, Python examples |
| `4-WIN_Software/` | Windows | CANVIEWER GUI, CANVIEWER-SDK, SavvyCAN-FD |
| `5_ThirdParty_Soft/` | — | Third-party software download link |
| `CE-FCC/` | — | CE / FCC certification documents |

---

## 1. Pibiger SDK

The **Pibiger SDK** (version 5.0.0) is the recommended choice for developers who need direct, low-level camera access and maximum performance. It provides a lightweight, cross-platform C/C++ API and a Python binding, all built on the same underlying shared library.

**SDK version**: 5.0.0 — **Last updated**: 2026-05-14

For full delivery notes and package contents, see [`1-Pibiger_SDK_WIN_Linux_Python/DELIVERY_OVERVIEW.md`](./1-Pibiger_SDK_WIN_Linux_Python/DELIVERY_OVERVIEW.md).

### Available Packages

| Package | Platform | Size | Description |
| :--- | :--- | :--- | :--- |
| `V5-SDK-DLL-CUS.zip` | Windows x64 | 19 MB (zip) / 45 MB | C/C++ SDK with GUI viewer (SAVVYCANFD.exe), CLI demo, headers, and bundled runtime |
| `V5-SDK-SO-CUS.tar.gz` | Linux x64 / ARM64 | 494 KB (tar.gz) / 1.3 MB | C/C++ SDK with GUI viewer, CLI demo, and headers |
| `V5-SDK-PYTHON-CUS.zip` | Windows + Linux x64 / ARM64 | 153 KB (zip) / 390 KB | Python SDK — bundles native libraries for all platforms |

All three packages share the same SDK source tree and the same underlying shared library. The Python package wraps the identical C library via ctypes — no separate codepath.

### Supported Platforms

| Platform | Architecture | Status |
| :--- | :--- | :--- |
| Windows 10 / 11 | x64 | ✅ Fully Supported |
| Ubuntu 22.04+ / Debian 12+ | x64 | ✅ Fully Supported |
| Raspberry Pi 5 (Bookworm) | ARM64 | ✅ Fully Supported |
| NVIDIA Jetson Orin Nano (Ubuntu 22.04) | ARM64 | ✅ Fully Supported |

### Supported Hardware Backends

| Backend | Platform | Hardware |
| :--- | :--- | :--- |
| libusb + gs_usb protocol | Windows / Linux | candleLight-compatible USB-CAN adapters |
| SocketCAN | Linux | Any kernel-supported CAN interface (`can0`, `vcan0`, etc.) |

### Windows Quick Start (C/C++)

```
1. Extract V5-SDK-DLL-CUS.zip to any directory (e.g., D:\usbcan\)
2. Plug in the USB-CAN adapter — Windows recognizes candleLight / gs_usb devices out-of-the-box, no driver install needed
3. Double-click run_SAVVYCANFD.bat → GUI launches and your adapter appears in the device list
```

For Windows driver guidance, see: [Quick Start Guide](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/quick-start-guide)

### Linux Quick Start (C/C++)

```bash
tar xzf V5-SDK-SO-CUS.tar.gz
cd V5-SDK-SO-CUS

# Install runtime dependencies (one-time)
sudo apt update && sudo apt install -y libusb-1.0-0 libqt6widgets6

# For candleLight / gs_usb USB adapters — non-root access via udev
sudo tee /etc/udev/rules.d/90-usbcan.rules > /dev/null <<'EOF'
SUBSYSTEM=="usb", ATTRS{idVendor}=="1d50", ATTRS{idProduct}=="606f", MODE="0666", GROUP="plugdev"
EOF
sudo udevadm control --reload-rules && sudo udevadm trigger
sudo usermod -aG plugdev $USER
# Log out and back in for the group change to take effect

# Launch the GUI viewer
case "$(uname -m)" in
    x86_64)  cd ubuntu22.04-x64 ;;
    aarch64) cd ubuntu22.04-arm64 ;;
esac
./run_SAVVYCANFD.sh
```

### Python SDK (V5-SDK-PYTHON-CUS)

The Python package targets **Python 3.8–3.12** on Windows x64, Linux x64, and Linux ARM64. It is ideal for test automation, ECU diagnostics scripts, data-logging, and Jupyter notebooks.

**Windows:**
```bat
:: 1. Extract V5-SDK-PYTHON-CUS.zip
:: 2. Open a command prompt in V5-SDK-PYTHON-CUS\
install_deps.bat        :: installs optional dependencies
run_basic_capture.bat   :: smoke test
run_recv_loop.bat       :: live receive loop
```

**Linux (Ubuntu 22.04, Debian 12+, Raspberry Pi OS Bookworm):**
```bash
# Same prerequisites as the C/C++ Linux package (libusb-1.0-0 + udev rule above)
unzip V5-SDK-PYTHON-CUS.zip
cd V5-SDK-PYTHON-CUS
chmod +x *.sh
./install_deps.sh
./run_basic_capture.sh
```

**Python API example:**
```python
import usb_can

# Discover adapters
for d in usb_can.discover():
    print(d.name, d.driver, d.serial)

# Open, configure, send, receive
with usb_can.Device(index=0) as dev:
    dev.configure(bitrate=500_000)        # 500 kbps classic CAN
    dev.start()
    dev.send(can_id=0x123, data=b'\x11\x22\x33\x44')
    for msg in dev.receive(timeout_ms=1000):
        print(f"{msg.id:08X}  {msg.data.hex()}  ts={msg.timestamp_us}")
```

**Optional dependencies:**

| Feature | Package | Install |
| :--- | :--- | :--- |
| Core (zero dependencies) | — | (nothing) |
| Test runner | `pytest` | `pip install pytest` |
| Notebook / plotting | `numpy`, `matplotlib` | `pip install numpy matplotlib` |

---

## 2. macOS SDK

A macOS SDK package is available in `2-MacOS_SDK/V5-SDK-MACOS-CUS.zip`.

For macOS installation and usage details, refer to the README inside the package.

---

## 3. Linux SocketCAN

For Linux users who prefer the native kernel SocketCAN interface, example code and can-utils are provided in `3_Linux_Soft_SocketCAN/`.

### Setup

```bash
sudo apt update && sudo apt install -y can-utils

# Bring up the CAN interface (replace can0 with your interface name)
sudo ip link set can0 up type can bitrate 500000
```

### C Examples

```bash
# Receive CAN FD frames
./3_Linux_Soft_SocketCAN/c/can0_receive_fd

# Send CAN FD frames
./3_Linux_Soft_SocketCAN/c/can1_send_fd
```

### Python Examples

```bash
# Receive
python3 3_Linux_Soft_SocketCAN/python3/receive.py

# Send
python3 3_Linux_Soft_SocketCAN/python3/send.py
```

### Common SocketCAN Commands

```bash
# Monitor CAN traffic
candump can0

# Send a CAN FD frame
cansend can0 123##0112233445566778899AABBCCDDEEFF

# List available CAN interfaces
ip link show type can
```

---

## 4. Windows Software

The following Windows GUI applications are provided in `4-WIN_Software/`:

| Application | Description |
| :--- | :--- |
| `SavvyCAN-FD.zip` | Advanced open-source CAN analysis tool with scripting support |

---

## 5. Third-Party Software

Additional third-party tools (Busmaster, etc.) are available for download:

**Download**: [https://www.jianguoyun.com/p/DfuYpksQpdSrBxjO-p0GIAA](https://www.jianguoyun.com/p/DfuYpksQpdSrBxjO-p0GIAA)  
**Password**: `hibqbp`

---

## Troubleshooting

**Windows — Device not detected**
- Refer to the [Quick Start Guide](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/quick-start-guide) for driver installation instructions specific to your adapter type.

**Linux — Permission denied accessing CAN interface**
- Add your user to the `plugdev` group: `sudo usermod -aG plugdev $USER`, then log out and back in.

**Linux — CAN interface not appearing**
- Ensure the device is connected and the SocketCAN driver is loaded: `sudo modprobe can_dev`

---

## Support

- **Website**: [www.pibiger-tech.com](https://www.pibiger-tech.com)
- **Documentation**: [docs.pibiger-tech.com](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd)
- **Email**: [support@pibiger-tech.com](mailto:support@pibiger-tech.com)

---

**SDK Version**: 5.0.0 — **Last Updated**: 2026-05-14
