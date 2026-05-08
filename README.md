# PIBIGER SavvyCAN-FD Series

**Professional USB-CAN FD Interface with CANVIEWER & SDK**

![License](https://img.shields.io/badge/License-Free-green) ![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-blue) ![Standard](https://img.shields.io/badge/Standard-SocketCAN%20%7C%20CAN%20FD-blue)

---

## 🎯 Overview

**PIBIGER SavvyCAN-FD Series** provides professional-grade USB interfaces for CAN/CAN FD bus communication. The series includes single-channel and dual-channel models designed for different application requirements. All models provide:

- **CANVIEWER** — A powerful GUI application for real-time CAN bus monitoring, analysis, and debugging
- **CANVIEWER-SDK** — A comprehensive C API for custom application development
- **SocketCAN Support** — Full Linux SocketCAN integration
- **CAN FD Compliance** — Support for high-speed CAN FD communication (up to 12 Mbit/s)
- **Professional Tools** — Includes SavvyCAN, Busmaster, and other industry-standard software

---

## ⭐ Key Features

- **SocketCAN Compatible** — Fully compatible SocketCAN devices for Linux systems
- **SavvyCAN Support** — Official SavvyCAN software support for CAN FD communication
- **Third-Party Compatibility** — Compatible with Busmaster, SocketCAN, and other standard tools
- **High-Speed Data Transfer** — Supports CAN FD bit rates from 25 kbit/s up to 12 Mbit/s maximum
- **Precision Timing** — Timestamp resolution up to 1 microsecond for accurate timing analysis
- **Robust Isolation** — Each CAN FD signal and power line separately isolated against USB up to 2.5 kV
- **Professional Analysis Tools** — Built-in message filtering, graphing, and protocol analysis
- **Cross-Platform** — Windows and Linux support with native drivers

---

## 🔧 Detailed Hardware Specifications

### Common Specifications (All Models)

| Specification | Details |
|---------------|----------|
| **CAN Standard** | CAN 2.0B / CAN FD |
| **Arbitration Bitrate** | 25 kbit/s to 1 Mbit/s |
| **Data Bitrate (FD)** | Up to 12 Mbit/s |
| **Timestamp Resolution** | 1 microsecond |
| **Galvanic Isolation** | 2.5 kV per channel (signal and power) |
| **Operating Temperature** | 0°C to 50°C |
| **Storage Temperature** | -20°C to 70°C |
| **Humidity** | 10% to 90% (non-condensing) |
| **Power Supply** | USB bus powered (5V) |
| **Power Consumption** | < 500 mA per channel |
| **USB Protocol** | USB 2.0 High-Speed (480 Mbps) |
| **Compliance** | CE, FCC certified |

### SavvyCAN-FD-C Specifications

| Specification | Details |
|---------------|----------|
| **Channels** | 1 × CAN/CAN FD |
| **Connectors** | USB Type-A, 1 × CAN D-Sub 9-pin |
| **Dimensions** | Compact desktop form factor |
| **Weight** | Lightweight portable |
| **Termination** | 120Ω termination resistor (switchable) |
| **LED Indicators** | Power, CAN Activity, Error status |

### SavvyCAN-FD-X2 Specifications

| Specification | Details |
|---------------|----------|
| **Channels** | 2 × CAN/CAN FD (fully independent) |
| **Connectors** | USB Type-A, 2 × CAN D-Sub 9-pin |
| **Dimensions** | Compact desktop form factor |
| **Weight** | Lightweight portable |
| **Termination** | 120Ω termination resistor per channel (switchable) |
| **LED Indicators** | Power, CAN1 Activity, CAN2 Activity, Error status |
| **Channel Isolation** | Complete electrical isolation between channels |
| **Simultaneous Operation** | Both channels can operate independently at different bitrates |

---

## 📚 Documentation

- **[Hardware Manual](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd#id-2-hardware-manual)** — Detailed hardware specifications and pinouts
- **[Quick Start Guide](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/quick-start-guide)** — Step-by-step instructions to get your device running
- **[CAN FD Protocol](https://docs.pibiger-tech.com/home/usb-to-can-fd-series/savvycanfd/can-fd-protocal)** — Information on CAN FD standard and data rates

---

## 📋 Product Models

The SavvyCAN-FD Series includes two main models:

### SavvyCAN-FD-C (Single Channel)

| Feature | Details |
|---------|----------|
| **Channels** | 1 × CAN/CAN FD |
| **Interface** | USB 2.0 High-Speed |
| **Bitrate** | 25 kbit/s - 12 Mbit/s |
| **Isolation** | 2.5 kV galvanic isolation |
| **Connectors** | USB Type-A, CAN D-Sub 9-pin |
| **Form Factor** | Compact desktop |
| **Power** | USB bus powered |
| **Applications** | Single CAN network monitoring, automotive diagnostics, embedded systems |
| **Product Link** | [View Product](https://www.pibiger-tech.com/product/savvycan-fd-c/) |

### SavvyCAN-FD-X2 (Dual Channel)

| Feature | Details |
|---------|----------|
| **Channels** | 2 × CAN/CAN FD (independent) |
| **Interface** | USB 2.0 High-Speed |
| **Bitrate** | 25 kbit/s - 12 Mbit/s (per channel) |
| **Isolation** | 2.5 kV galvanic isolation (per channel) |
| **Connectors** | USB Type-A, 2 × CAN D-Sub 9-pin |
| **Form Factor** | Compact desktop |
| **Power** | USB bus powered |
| **Applications** | Multi-network monitoring, CAN gateway, network bridging, complex automotive systems |
| **Product Link** | [View Product](https://www.pibiger-tech.com/product/savvycan-fd-x2/) |

---

## 📦 What's Included

### Windows Software

| Component | Details |
|-----------|---------|
| **CANVIEWER** | Professional GUI for CAN bus monitoring and analysis |
| **CANVIEWER-SDK** | C API for custom Windows applications |
| **SavvyCAN** | Advanced CAN analysis and scripting tool |
| **Busmaster** | Open-source CAN network design and simulation software |
| **Drivers** | WinUSB drivers (bundled with Zadig installer) |

### Linux Software

| Component | Details |
|-----------|---------|
| **can-utils** | Standard SocketCAN utilities (candump, cansend, etc.) |
| **SocketCAN** | Native Linux kernel CAN support |
| **udev Rules** | Automatic device recognition and permissions |

---

## 🚀 Quick Start

### Windows

#### 1. Install WinUSB Driver

```
1. Extract the repository
2. Run: 2-WIN_Software/tools/zadig-2.9.exe as Administrator
3. Select your PIBIGER USB-CAN device
4. Click "Replace Driver" to install WinUSB
5. Restart the computer (recommended)
```

#### 2. Launch CANVIEWER

```
Double-click: 2-WIN_Software/Release/canviewer.exe
```

The GUI should launch and automatically detect connected CAN devices.

### Linux

#### 1. Install SocketCAN Tools

```bash
sudo apt update
sudo apt install -y can-utils
```

#### 2. Load SocketCAN Driver

```bash
# For PIBIGER USB-CAN devices
sudo modprobe can_dev
sudo modprobe can_usb
```

#### 3. View CAN Traffic

```bash
# List available CAN interfaces
ip link show

# Monitor CAN traffic
candump can0

# Send a CAN message
cansend can0 123#1122334455667788
```

---

## 💻 CANVIEWER GUI Application

### Features

- **Real-time Monitoring** — Live CAN bus traffic visualization
- **Message Filtering** — Advanced filtering by ID, data patterns, and frame types
- **Graphing** — Plot CAN signals over time
- **Message Logging** — Record and replay CAN traffic
- **Protocol Analysis** — Built-in support for common automotive protocols
- **Trigger & Capture** — Capture specific message sequences
- **Data Export** — Export to CSV, DBC, and other formats

### User Interface

```
┌─────────────────────────────────────────────────┐
│ CANVIEWER - CAN Bus Monitor & Analyzer          │
├─────────────────────────────────────────────────┤
│ Device: [PIBIGER USB-CAN FD v1.0]  [Connect]   │
├─────────────────────────────────────────────────┤
│ Bitrate: 500 kbps  |  Frames: 1,234  |  Errors: 0
├─────────────────────────────────────────────────┤
│ ID      | DLC | Data                | Time      │
│ 0x123   | 8   | 11 22 33 44 55 66 77 88 | 12:34:56│
│ 0x456   | 4   | AA BB CC DD          | 12:34:57│
│ 0x789   | 2   | FF EE                | 12:34:58│
├─────────────────────────────────────────────────┤
│ [Save] [Load] [Clear] [Export] [Settings]      │
└─────────────────────────────────────────────────┘
```

### Quick Start

1. **Connect Device**: Click "Connect" and select your PIBIGER device
2. **Set Bitrate**: Choose 250k, 500k, 1M, or custom value
3. **Monitor Traffic**: Messages appear in real-time as they arrive
4. **Filter Messages**: Use ID range or data pattern filters
5. **Log Data**: Click "Record" to save traffic to file
6. **Analyze**: Use graphing and protocol analysis tools

---

## 🔧 CANVIEWER-SDK (C API)

### Overview

The **CANVIEWER-SDK** provides a simple, cross-compiler-friendly C API for developing custom CAN applications.

### Key Features

- **Simple C API** — Easy-to-use functions for CAN communication
- **Device Discovery** — Automatically find connected CAN devices
- **Message Filtering** — Hardware-level frame filtering
- **Statistics** — Real-time bus statistics and error monitoring
- **CAN FD Support** — Full support for CAN FD frames (up to 64 bytes)
- **Microsecond Timestamps** — Precise timing for time-critical applications

### SDK Structure

```
V5-SDK-DLL-CUS/
├── README.md                     SDK documentation
├── DEVELOPMENT.md                Development guide
├── bin/
│   ├── usb_can.dll              SDK library
│   └── can_example.exe          Example application
├── lib/
│   └── usb_can.lib              Import library (for linking)
├── include/can/
│   ├── usb_can_sdk.h            Main header file
│   ├── can_types.h              Type definitions
│   └── can_device.h             Device control API
└── example/
    └── basic_can.c              Complete example code
```

### Basic Workflow

```c
#include "can/usb_can_sdk.h"
#include <stdio.h>

int main(void) {
    /* 1. Initialize SDK */
    can_sdk_init();

    /* 2. Discover devices */
    can_device_info_t devices[8];
    int count = can_discover(devices, 8);
    if (count <= 0) {
        printf("No CAN devices found.\n");
        return 1;
    }

    /* 3. Open first device */
    can_handle_t handle;
    can_open(&handle, devices[0].index);

    /* 4. Configure CAN parameters */
    can_config_t config = {0};
    config.bitrate = 500000;  /* 500 kbps */
    can_configure(handle, &config);

    /* 5. Start communication */
    can_start(handle);

    /* 6. Send a CAN message */
    can_msg_t tx_msg = {0};
    tx_msg.id = 0x123;
    tx_msg.dlc = 8;
    for (int i = 0; i < 8; i++) tx_msg.data[i] = i;
    can_send(handle, &tx_msg);

    /* 7. Receive messages */
    can_msg_t rx_msgs[16];
    int rx_count = can_receive(handle, rx_msgs, 16, 1000);
    for (int i = 0; i < rx_count; i++) {
        printf("RX ID=0x%X DLC=%u\n", rx_msgs[i].id, rx_msgs[i].dlc);
    }

    /* 8. Cleanup */
    can_stop(handle);
    can_close(handle);
    can_sdk_shutdown();

    return 0;
}
```

### Compilation (Windows)

#### Using MSVC Command Line

```cmd
cl your_app.c /I path\to\include /link path\to\lib\usb_can.lib
copy path\to\bin\usb_can.dll .
your_app.exe
```

#### Using CMake

```cmake
cmake_minimum_required(VERSION 3.16)
project(my_can_app LANGUAGES C)

set(SDK_DIR path/to/V5-SDK-DLL-CUS)

add_executable(my_app main.c)
target_include_directories(my_app PRIVATE ${SDK_DIR}/include)
target_link_libraries(my_app PRIVATE ${SDK_DIR}/lib/usb_can.lib)

# Copy DLL to output directory
add_custom_command(TARGET my_app POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        ${SDK_DIR}/bin/usb_can.dll $<TARGET_FILE_DIR:my_app>)
```

### Core API Functions

#### Initialization & Discovery

```c
can_status_t can_sdk_init(void);
void         can_sdk_shutdown(void);
int          can_discover(can_device_info_t *devices, int max_count);
```

#### Device Control

```c
can_status_t can_open(can_handle_t *handle, int device_index);
void         can_close(can_handle_t handle);
can_status_t can_start(can_handle_t handle);
can_status_t can_stop(can_handle_t handle);
```

#### Configuration

```c
can_status_t can_configure(can_handle_t handle, const can_config_t *config);
can_status_t can_get_config(can_handle_t handle, can_config_t *config);
```

#### Message Transfer

```c
can_status_t can_send(can_handle_t handle, const can_msg_t *msg);
int          can_receive(can_handle_t handle, can_msg_t *msgs, 
                         int max_count, uint32_t timeout_ms);
```

#### Statistics & Diagnostics

```c
can_status_t can_get_stats(can_handle_t handle, can_stats_t *stats);
can_status_t can_reset_stats(can_handle_t handle);
const char*  can_status_str(can_status_t status);
```

### Data Structures

#### CAN Message

```c
typedef struct {
    uint32_t id;            /* CAN ID (11-bit or 29-bit) */
    uint8_t  dlc;           /* Data length (0-8 or CAN FD 0-64) */
    uint8_t  flags;         /* Flags (CAN_FLAG_*) */
    uint8_t  data[64];      /* Message data */
    uint64_t timestamp_us;  /* Microsecond timestamp */
} can_msg_t;
```

#### Configuration

```c
typedef struct {
    uint32_t bitrate;           /* Arbitration bitrate (e.g., 500000) */
    uint32_t sample_point;      /* Sample point (1000=100%, 875=87.5%) */
    uint8_t  canfd_enabled;     /* 0=Classic CAN, 1=CAN FD */
    uint32_t data_bitrate;      /* FD data bitrate */
    uint32_t data_sample_point; /* FD data sample point */
} can_config_t;
```

### Common Tasks

#### 1. Send a Standard CAN Message

```c
can_msg_t msg = {0};
msg.id = 0x100;
msg.dlc = 2;
msg.data[0] = 0xAA;
msg.data[1] = 0xBB;
can_send(handle, &msg);
```

#### 2. Send Extended Frame (29-bit ID)

```c
can_msg_t msg = {0};
msg.id = 0x18FF50E0;
msg.dlc = 8;
msg.flags = CAN_FLAG_EXTENDED;
can_send(handle, &msg);
```

#### 3. Send CAN FD Frame

```c
can_config_t cfg = {0};
cfg.bitrate = 500000;
cfg.canfd_enabled = 1;
cfg.data_bitrate = 2000000;
can_configure(handle, &cfg);
can_start(handle);

can_msg_t fd_msg = {0};
fd_msg.id = 0x200;
fd_msg.dlc = 64;  /* Full CAN FD payload */
fd_msg.flags = CAN_FLAG_FD | CAN_FLAG_BRS;
can_send(handle, &fd_msg);
```

#### 4. Blocking Receive with Timeout

```c
can_msg_t buffer[32];
int count = can_receive(handle, buffer, 32, 100);  /* 100ms timeout */
for (int i = 0; i < count; i++) {
    printf("[%llu us] ID=0x%X DLC=%u\n", 
           (unsigned long long)buffer[i].timestamp_us,
           buffer[i].id, buffer[i].dlc);
}
```

#### 5. Monitor Bus State

```c
can_stats_t stats;
can_get_stats(handle, &stats);
if (stats.bus_state == CAN_STATE_BUS_OFF) {
    printf("Bus-off detected! Resetting...\n");
    can_reset(handle);
    can_start(handle);
}
```

---

## 📚 Third-Party Software

### SavvyCAN

Advanced CAN analysis and scripting platform with:
- Message filtering and graphing
- Protocol decoding (UDS, J1939, ISO-TP)
- Scripting interface for automation
- Real-time data visualization

**Download:** Included in `2-WIN_Software/SavvyCAN-FD.zip`

### Busmaster

Open-source CAN network design and simulation software:
- Message generation and transmission
- Bus monitoring and analysis
- Protocol simulation
- Network testing

**Download:** Available in `4_ThirdParty_Soft/` folder

---

### Supported Hardware

**PIBIGER SavvyCAN-FD Series** — All models fully supported

| Model | Channels | Bitrate | Features | Certifications |
|-------|----------|---------|----------|----------------|
| **SavvyCAN-FD-C** | 1 | 25 kbit/s - 12 Mbit/s | Single channel, compact | CE, FCC |
| **SavvyCAN-FD-X2** | 2 | 25 kbit/s - 12 Mbit/s | Dual channel, independent | CE, FCC |

### Platform Compatibility

- **Windows 10/11** x64
- **Linux** (Ubuntu 22.04+, Debian 12+, Raspberry Pi OS)
- **SocketCAN** compliant
- **CAN FD** standard compliantt

---

## 📋 System Requirements

### Windows

- **OS:** Windows 10 (build 1809+) or Windows 11 x64
- **USB:** USB 2.0 or higher
- **Driver:** WinUSB (installed via Zadig)
- **Runtime:** Bundled (Qt6, libusb)

### Linux

- **OS:** Ubuntu 22.04 LTS or newer, Debian 12+
- **USB:** USB 2.0 or higher
- **Packages:** `can-utils`, `libusb-1.0-0`
- **Compiler:** GCC 11+ (for SDK development)

---

## 🛠️ Troubleshooting

### Windows

**Issue:** Device not detected
- **Solution:** Ensure WinUSB driver is installed using Zadig. Check Device Manager for the device.

**Issue:** CANVIEWER won't start
- **Solution:** Verify all DLL files are in the same directory. Run as Administrator if needed.

**Issue:** "usb_can.dll not found"
- **Solution:** Copy `usb_can.dll` from `bin/` to your application directory.

### Linux

**Issue:** Permission denied accessing CAN interface
- **Solution:** Add your user to the `dialout` group: `sudo usermod -aG dialout $USER`

**Issue:** CAN interface not appearing
- **Solution:** Ensure the device is connected and SocketCAN driver is loaded: `sudo modprobe can_dev can_usb`

---

## 📞 Support & Documentation

- **SDK Documentation:** See `2-WIN_Software/V5-SDK-DLL-CUS/README.md`
- **Development Guide:** See `2-WIN_Software/V5-SDK-DLL-CUS/DEVELOPMENT.md`
- **Example Code:** See `2-WIN_Software/V5-SDK-DLL-CUS/example/basic_can.c`
- **Technical Support:** Contact PIBIGER support team

---

## 🔗 Related Resources

- [CAN FD Standard](https://www.can-cia.org/can-knowledge/can/can-fd/)
- [SocketCAN Documentation](https://www.kernel.org/doc/html/latest/networking/can.html)
- [Zadig USB Driver Installer](https://zadig.akeo.ie/)

---

**Last Updated:** May 8, 2026  
**SDK Version:** 5.0  
**Status:** ✅ Production Ready
