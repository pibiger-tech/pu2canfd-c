# PIBIGER SavvyCAN-FD Series

**Professional USB-CAN FD Interface with CANVIEWER & SDK**

![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue) ![Standard](https://img.shields.io/badge/Standard-SocketCAN%20%7C%20CAN%20FD-blue)

---

## Overview

**PIBIGER SavvyCAN-FD Series** provides professional-grade USB interfaces for CAN/CAN FD bus communication. The series includes single-channel and dual-channel models designed for different application requirements.

- **SAVVYCANFD GUI** — Real-time CAN bus monitoring, analysis, and debugging
- **SAVVYCANFD SDK** — Cross-platform C/C++ and Python API for custom application development
- **SocketCAN Support** — Full Linux SocketCAN integration
- **CAN FD Compliance** — Up to 12 Mbit/s data bitrate

---

## Key Specifications

| Specification | Details |
| :--- | :--- |
| **CAN Standard** | CAN 2.0B / CAN FD |
| **Arbitration Bitrate** | 25 kbit/s – 1 Mbit/s |
| **Data Bitrate (FD)** | Up to 12 Mbit/s |
| **Timestamp Resolution** | 1 µs |
| **Galvanic Isolation** | 2.5 kV per channel |
| **Power Supply** | USB bus powered (5V) |
| **USB Protocol** | USB 2.0 High-Speed (480 Mbps) |
| **Compliance** | CE, FCC |
| **Operating Temperature** | 0°C to 50°C |

---

## Product Models

| Model | Channels | Connector |
| :--- | :--- | :--- |
| **SavvyCAN-FD-C** | 1 × CAN/CAN FD | USB Type-A + 1 × D-Sub 9-pin |
| **SavvyCAN-FD-X2** | 2 × CAN/CAN FD (independent) | USB Type-A + 2 × D-Sub 9-pin |

---

## Repository Structure

| Directory / File | Description |
| :--- | :--- |
| [`1-Pibiger_SDK_WIN_Linux_Python_MacOS/`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/) | Pibiger SDK packages for Windows, Linux x64/ARM64, macOS, and Python |
| [`1-Pibiger_SDK_WIN_Linux_Python_MacOS/DELIVERY_OVERVIEW.md`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/DELIVERY_OVERVIEW.md) | Full SDK documentation: installation, API reference, and code examples |
| [`1-Pibiger_SDK_WIN_Linux_Python_MacOS/RELEASE_NOTES.md`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/RELEASE_NOTES.md) | SDK changelog and version history |
| [`2-Driver/Win/`](./2-Driver/Win/) | Windows driver download link |
| [`2-Driver/Mac/`](./2-Driver/Mac/) | macOS Python SDK package |
| [`3_Linux_Soft_SocketCAN/`](./3_Linux_Soft_SocketCAN/) | Linux SocketCAN C and Python examples, can-utils |
| [`4-WIN_Software/`](./4-WIN_Software/) | SavvyCAN-FD Windows GUI application |
| [`5_ThirdParty_Soft/`](./5_ThirdParty_Soft/) | Third-party software download link (Busmaster, etc.) |
| [`CE-FCC/`](./CE-FCC/) | CE and FCC certification documents |

---

## SDK Packages

For full installation instructions, supported platforms, API reference, and code examples, see:

> **[`1-Pibiger_SDK_WIN_Linux_Python_MacOS/DELIVERY_OVERVIEW.md`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/DELIVERY_OVERVIEW.md)**

| Package | Platform |
| :--- | :--- |
| [`SAVVYCANFD-Windows-x64.zip`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-Windows-x64.zip) | Windows 10/11 x64 |
| [`SAVVYCANFD-Linux-x64.tar.gz`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-Linux-x64.tar.gz) | Ubuntu 22.04+ x64 |
| [`SAVVYCANFD-Linux-arm64.tar.gz`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-Linux-arm64.tar.gz) | Raspberry Pi 5 / Jetson Orin Nano (ARM64) |
| [`SAVVYCANFD-macOS-arm64.zip`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-macOS-arm64.zip) | macOS — Apple Silicon (M1–M4) |
| [`SAVVYCANFD-macOS-x64.zip`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-macOS-x64.zip) | macOS — Intel |
| [`SAVVYCANFD-Python.zip`](./1-Pibiger_SDK_WIN_Linux_Python_MacOS/SAVVYCANFD-Python.zip) | Python 3.8+ — all platforms |

---

## Documentation

- **[Hardware Manual & Quick Start Guide](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd)** — Hardware specifications, pinouts, and step-by-step setup
- **[CAN FD Protocol](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/can-fd-protocal)** — CAN FD standard and data rate reference

---

## Support

- **Website**: [www.pibiger-tech.com](https://www.pibiger-tech.com)
- **Documentation**: [docs.pibiger-tech.com](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd)
- **Email**: [support@pibiger-tech.com](mailto:support@pibiger-tech.com)
