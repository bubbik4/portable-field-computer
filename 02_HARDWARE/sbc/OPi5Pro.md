---
title: OPi5Pro
type: hardware
category: sbc
status: To be reviewed
project_revision: R0
created: 2026-11-08
updated: 2026-11-08
tags:
  - hardware
---

# OPi5Pro

## 1. Overview

The Orange Pi 5 Pro is the currently selected main computing platform for the project.
It is an ARM-based single-board computer built around the Rockchip RK3588S SoC.
The board was selected due to its combination of processing capabilities, integrated wireless connectivity, NVMe storage support, compact dimensions and GPIO expansion.
	
### Selection Status

| Property            | Value            |
| ------------------- | ---------------- |
| Component           | Orange Pi 5 Pro  |
| RAM Configuration   | 8 GB LPDDR5      |
| SoC                 | Rockchip RK3588S |
| Project Revision    | R0               |
| Selection Status    | Selected         |
| Hardware Validation | Not Tested       |
| Purchase Status     | Pending          |

This selection represents the current project baseline. Final validation will take place after acquiring and testing the board.

## 2. Technical Specifications

### 2.1 Processor

| Property                           | Specification                 |
| ---------------------------------- | ----------------------------- |
| SoC                                | Rockchip RK3588S              |
| Architecture                       | ARM64                         |
| CPU Configuration                  | 4x Cortex-A76 + 4x Cortex-A55 |
| Maximum Performance Core Frequency | 2.4 GHz                       |
| Maximum Efficiency Core Frequency  | 1.8 GHz                       |
| Manufacturing Process              | 8 nm                          |
|                                    |                               |

### 2.2 Graphics and AI

|Property|Specification|
|---|---|
|GPU|ARM Mali-G610 MP4|
|NPU|Up to 6 TOPS|
|Graphics APIs|OpenGL ES, OpenCL, Vulkan|

Hardware acceleration and GPU driver functionality must be verified with the selected Linux image.

### 2.3 Memory

|Property|Specification|
|---|---|
|Capacity|8 GB|
|Technology|LPDDR5|
|Configuration|Onboard memory|
|Upgradeability|Not upgradeable|

The 8 GB configuration is considered sufficient for the planned Linux desktop, networking tools, SDR applications and custom software.

### 2.4 Storage

|Interface|Specification|
|---|---|
|M.2|M-Key|
|M.2 Form Factor|2280|
|PCIe Interface|PCIe 2.0 x1|
|Theoretical Maximum Throughput|Approximately 500 MB/s|
|eMMC|Dedicated module connector|
|MicroSD|Supported|
|SPI Flash|16 MB, default configuration to be verified|

An NVMe SSD is the preferred primary storage solution.

The PCIe interface limits the maximum performance of faster NVMe drives. Purchasing an expensive high-performance PCIe 4.0 SSD is therefore unnecessary.

### 2.5 Networking

|Interface|Specification|
|---|---|
|Ethernet|Gigabit Ethernet|
|Wireless|Wi-Fi 5 (802.11ac)|
|Bluetooth|Bluetooth 5.0 / BLE|

Integrated wireless connectivity eliminates the need for an additional Wi-Fi adapter during initial prototyping.

External USB network adapters may be added if additional interfaces are required.

### 2.6 Display Interfaces

|Interface|Specification|
|---|---|
|HDMI 1|HDMI 2.1, up to 8K@60Hz|
|HDMI 2|HDMI 2.0, up to 4K@60Hz|
|MIPI DSI|4-lane|
|USB-C DisplayPort Alt Mode|Not supported|

The USB-C connector is used for power input and flashing, not DisplayPort video output.

The planned primary display will use HDMI, with a separate USB connection for touchscreen input.

### 2.7 USB and Expansion

|Interface|Specification|
|---|---|
|USB 3.x|1x|
|USB 2.0|3x|
|GPIO|40-pin expansion header|
|UART|Supported|
|I2C|Supported|
|SPI|Supported|
|PWM|Supported|
|CAN|Supported|

The GPIO header will provide the interface for future hardware expansion and communication with the auxiliary microcontroller.

Electrical compatibility and pin assignments must be verified before connecting external hardware.

### 2.8 Physical Dimensions

|Property|Value|
|---|---|
|Length|89 mm|
|Width|56 mm|
|Weight|Approximately 58 g|
|Mounting|Custom enclosure|

The board's compact footprint is particularly suitable for the planned portable clamshell enclosure.

---

## 3. Why This Platform Was Selected

### 3.1 Processing Performance

The RK3588S provides an eight-core ARM CPU with a combination of high-performance and efficiency cores.

This provides sufficient processing headroom for:
- Linux desktop environment.
- Network diagnostics.
- SDR applications.
- Multiple concurrent applications.
- Custom system dashboard.
- Background services and automation.

### 3.2 Integrated Connectivity

The board provides onboard Wi-Fi and Bluetooth, Gigabit Ethernet and multiple USB interfaces. This reduces the number of additional modules required for the initial configuration.

### 3.3 NVMe Storage

The integrated M.2 M-Key connector supports standard 2280 NVMe drives. This allows the system to use internal solid-state storage without an external adapter or additional expansion board.

### 3.4 Compact Form Factor

The 89 x 56 mm footprint simplifies mechanical integration and enclosure design. The 40-pin GPIO header also provides a familiar expansion interface.

### 3.5 Performance-to-Cost Balance

The Orange Pi 5 Pro provides a strong combination of processing performance, memory bandwidth, integrated peripherals and storage expansion. It was selected as the preferred balance between hardware capabilities, physical dimensions and the project's available budget.

---

## 4. Limitations and Risks

### 4.1 Linux Compatibility

Linux support is less standardized than on the Raspberry Pi platform. Different kernel branches and distributions may provide different levels of hardware functionality. GPU acceleration, Wi-Fi, Bluetooth, GPIO and peripheral compatibility must be tested with the selected operating system.

### 4.2 Power Requirements

The board requires a stable 5V power supply. The manufacturer recommends a 5V / 5A USB-C power source. Higher USB-C PD voltages must not be connected directly to the board's 5V input. The project's power distribution system must provide a regulated 5V output with sufficient current capacity.

### 4.3 Thermal Management

The RK3588S can generate considerable heat under sustained CPU and GPU workloads. The final enclosure must provide adequate thermal management. A heatsink and controlled active cooling are planned, subject to thermal testing.

### 4.4 NVMe Performance

The M.2 interface operates at PCIe 2.0 x1. This limits the theoretical throughput to approximately 500 MB/s.

### 4.5 Display Connectivity

The USB-C connector does not provide DisplayPort Alt Mode. The primary display must therefore use HDMI or MIPI DSI.

---

## 5. Planned Project Integration

### 5.1 Main Computing Unit

The Orange Pi 5 Pro will serve as the central computing platform.

Responsibilities:

- Operating system execution.
- Application processing.
- Network administration.
- Storage management.
- SDR software.
- User interface.
- Communication with auxiliary hardware.

### 5.2 Auxiliary Controller

The Seeed Studio XIAO ESP32-C6 is planned as a separate hardware controller.

Potential responsibilities:
- Physical button inputs.
- Status indicators.
- Fan control.
- Temperature monitoring.
- Auxiliary system telemetry.
- Communication with the main SBC.

The preferred initial communication interface is USB Serial.

### 5.3 Display

Planned configuration
- 8-inch primary display.
- HDMI video connection.
- USB touchscreen connection.
- 1280 x 800 target resolution.

Final display model: TBD.

### 5.4 Storage

Planned configuration
- M.2 2280 NVMe SSD.
- Initial capacity: 256–512 GB.
- Linux operating system installed on NVMe.

Final SSD model: TBD.

### 5.5 Power

Initial development configuration.
- External USB-C PD power source.
- Regulated 5V power output.
- Dedicated power distribution.
- Separate power monitoring for auxiliary components.

Final power architecture: TBD.

---

## 6. Operating System

### Preferred Candidate

Armbian.
Armbian currently provides Orange Pi 5 Pro images using both vendor and current kernel branches.
The board is listed under community-supported hardware.
The final distribution and kernel branch will be selected after testing.

### Planned Desktop Environment

XFCE.
Reasons:

- Relatively lightweight.
- Suitable for an 8 GB ARM system.
- Familiar Linux desktop workflow.
- Suitable for diagnostic and administration tools.

---

## 7. Hardware Validation Plan

The board must pass the following tests before being considered verified.

### Initial Boot

- [ ] Verify power supply stability.
- [ ] Verify successful boot.
- [ ] Verify operating system installation.
- [ ] Verify system restart and shutdown.
- [ ] Verify storage detection.

### Storage

- [ ] Verify NVMe detection.
- [ ] Verify NVMe read/write performance.
- [ ] Verify boot from NVMe.
- [ ] Verify storage stability under sustained load.

### Networking

- [ ] Verify Gigabit Ethernet.
- [ ] Verify Wi-Fi connectivity.
- [ ] Verify Bluetooth connectivity.
- [ ] Test simultaneous network interfaces.

### Display

- [ ] Verify HDMI output.
- [ ] Verify 1280 x 800 resolution.
- [ ] Verify touchscreen input.
- [ ] Verify display rotation if required.
- [ ] Verify GPU acceleration.

### GPIO and Communication

- [ ] Verify GPIO functionality.
- [ ] Verify UART communication.
- [ ] Verify I2C communication.
- [ ] Verify SPI functionality.
- [ ] Establish USB Serial communication with XIAO ESP32-C6.

### Thermal and Power

- [ ] Measure idle power consumption.
- [ ] Measure power consumption under load.
- [ ] Monitor CPU temperature.
- [ ] Monitor GPU temperature if available.
- [ ] Test sustained CPU load.
- [ ] Test sustained GPU load.
- [ ] Verify cooling efficiency.

---

## 8. Open Issues

|ID|Issue|Status|
|---|---|---|
|OPI-001|Select Linux distribution|Open|
|OPI-002|Select NVMe SSD|Open|
|OPI-003|Select cooling solution|Open|
|OPI-004|Verify USB-C PD power architecture|Open|
|OPI-005|Select primary display|Open|
|OPI-006|Verify GPIO compatibility|Open|
|OPI-007|Verify GPU acceleration|Open|

---

## 9. Sources

Primary technical reference:
- Orange Pi 5 Pro User Manual, version 1.1.
- Official Orange Pi documentation.

Software support reference:
- Armbian Orange Pi 5 Pro board page.
- Armbian build documentation.

All specifications should be rechecked against the exact board revision and documentation available at the time of purchase.

---

## 10. References

## 11. Change History

| Date       | Description                    |
| ---------- | ------------------------------ |
| 2026-11-08 | Initial hardware documentation |