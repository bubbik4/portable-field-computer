# SBC Platform research

## Research objective

Indetify a suitable ARM single-board computer for the portable field computer project.

## Evaluation Criteria

- CPU performance
- GPU capabilities
- RAM capacity
- Storage interfaces
- Power consumption
- Thermal requirements
- Linux compatibility
- Peripheral connectivity
- Availability and price

## Candidates

### **Raspberry Pi 5**

Status: Under Review

Advantages:
- Unmatched Linux & Software compatibility
- Standardized form factor & ecosystem, huge selection of mechanical mounts, active coolers, HDMI displays, and HAT+ expansions
- RP1 I/O Controller with dedicated southbridge provides reliable USB 3.0 bandwidth
- Built-in wireless 802.11ac and Bluetooth 5.0/BLE

Disadvantages:
- Older 16nm litography (BCM2712) - causes higher idle power consumption (~2.7-3W) and higher thermal output under sustained load compared to 8nm Rockchip alternatives.
- Non-standard USB-C PD Profile: Requires 5V/5A (25W) USB-C PD profile for full peripheral current limit (1.6A on USB); Standard 9V/12V/15V/20V PD powerbanks without a 5V/5A profile default to a 600mA USB current limit unless overridden or powered via an external 5V buck converter.
- No native onboard M2. slot - requires additional PCIe FPC ribbon and M.2 HAT+ adapter to use NVMe SSD storage.

Notes:
Best choice if software stability and rapid prototyping outweigh raw multi-core performance and compact NVMe mounting.

---
### Orange Pi 5

Status: Under Review

Advantages:
- Superior 8nm SoC efficiency & performance (RK3588S): 8-core big.LITTLE architecture delivers roughly 1.5x-2x multi-core CPU performance over RPi 5 while maintaining lower idle power (~1.5W-1.8W).
- Strong GPU and NPU: Mali-G610 MP4 GPU handles full Linux GUI, hardware video encoding up to 8k@60 and waterfall plots effortlessly. Icludes 6 TOPS NPU for local egde AI tasks.
- Native onboard M.2 Slot on the bottom of the board.
- Full size HDMI 2.1 + DisplayPort 1.4 (via USB-C) + MIPI-DSI  interfaces

Disadvantages:
- No built-in Wi-Fi/BT on the base model
- Fragmented Linux Support
- Fixed 5V input - does not negotiate higher voltage USB-C PD profiles natively.

Notes:
- If selecting this family, the **Orange Pi 5 Pro** (LPDDR5, onboard Wi-Fi 5/BT 5.0, M.2 2280, RPi-like 89x56mm footprint) is strongly preferred over the original base Orange Pi 5 for a portable field terminal.

### Radxa ROCK 5B

Status: Under Review

Advantages:
- Full-Fledged RK3588 (Non-S) I/O Capabilities: Features a full PCIe 3.0 x4 M.2 2280 NVMe slot on the bottom AND a separate M.2 E-Key slot on the top for Wi-Fi 6E / Bluetooth 5.2 modules.
- Rich Connectivity for Field Diagnostics: Onboard 2.5 GbE RJ45 port, 2x full-size HDMI 2.1 outputs, 1x micro-HDMI input (allows using the field computer as a portable KVM/capture monitor in the field!), and USB-C with DisplayPort Alt Mode.
- Native USB-C PD Negotiation: Supports USB-C PD 2.0 (9V/2A, 12V/2A, 15V/2A, 20V/2A) directly on the board, aligning directly with *DEC-002* (initial prototyping with an external USB-C PD power source).
- High RAM Ceiling: Available in 4 GB, 8 GB, 16 GB, and 32 GB LPDDR4X (or LPDDR5 on ROCK 5B+).

Disadvantages:
- Larger Pico-ITX Footprint (100 x 72 mm): Takes up ~30% more planar space inside the enclosure compared to Raspberry Pi 5 (85 x 56 mm).
- Early USB-C PD Firmware Quirks: Requires careful selection of USB-C PD power banks or a fixed-voltage PD trigger cable if the power bank renegotiates voltage during boot before the OS loads.
- Higher Cost: **The most expensive board among the three candidates** (especially when factoring in the M.2 E-Key Wi-Fi/BT card if not buying the 5B+ variant).

Notes:
- The micro-HDMI **input** port is a unique killer feature for an IT/field administrator terminal, enabling the device to act as a portable crash-cart display for headless servers and network gear.

## Comparison

| Criterium                     | Raspberry Pi 5 (8 GB)                                                      | Orange Pi 5 / 5 Pro (8 GB)                                                         | Radxa ROCK 5B (8 GB)                                                                            |
| :---------------------------- | :------------------------------------------------------------------------- | :--------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------- |
| **SoC & Process**             | Broadcom BCM2712 (16nm)                                                    | Rockchip RK3588S (8nm)                                                             | Rockchip RK3588 (8nm)                                                                           |
| **CPU Performance**           | 4x Cortex-A76 @ 2.4 GHz (Good single-core, moderate multi-core)            | 4x A76 @ 2.4 GHz + 4x A55 @ 1.8 GHz (~1.7x faster multi-core)                      | 4x A76 @ 2.4 GHz + 4x A55 @ 1.8 GHz (~1.8x faster multi-core)                                   |
| **GPU & NPU**                 | VideoCore VII @ 800 MHz (OpenGL ES 3.1, Vulkan 1.2), No NPU                | Mali-G610 MP4 + 6 TOPS NPU                                                         | Mali-G610 MP4 + 6 TOPS NPU                                                                      |
| **RAM Capacity**              | 4 GB / 8 GB / 16 GB LPDDR4X                                                | 4 GB / 8 GB / 16 GB LPDDR4/4X (LPDDR5 on Pro)                                      | 4 GB / 8 GB / 16 GB / 32 GB LPDDR4X (LPDDR5 on 5B+)                                             |
| **Storage Interfaces**        | microSD + 1x PCIe 2.0 x1 (via FPC ribbon + HAT)                            | microSD, SPI Flash + M.2 NVMe (PCIe 2.0 x1)                                        | microSD, eMMC socket + M.2 2280 NVMe (PCIe 3.0 x4)                                              |
| **Power Consumption**         | Idle: ~2.7W / Load: ~8–12W (5V/5A USB-C)                                   | Idle: ~1.8W / Load: ~8–10W (5V/4A USB-C)                                           | Idle: ~2.5W / Load: ~10–14W (USB-C PD 9V–20V)                                                   |
| **Thermal Requirements**      | Requires active cooling (Official Active Cooler) under continuous load     | Runs cooler in light tasks; requires low-profile heatsink + PWM fan for heavy load | Requires dedicated heatsink + PWM fan when running NVMe + full CPU load                         |
| **Linux Compatibility**       | **10/10** – Official RPi OS, Debian, Ubuntu, Kali; full mainline support   | **7.5/10** – Armbian / Ubuntu Rockchip (Kernel 6.1 BSP / Mainline improving)       | **8/10** – Radxa OS (Debian), Armbian, Collabora Mainline Linux support                         |
| **Peripheral & Display I/O**  | 2x micro-HDMI, 2x MIPI DSI/CSI, 2x USB 3.0, 2x USB 2.0, 1 GbE, 40-pin GPIO | HDMI 2.1, DP 1.4 (USB-C), MIPI DSI, 1x USB 3.0, 2x USB 2.0, 1 GbE, 26/40-pin GPIO  | 2x HDMI 2.1 out, **1x micro-HDMI IN**, DP (USB-C), 2x USB 3.0, 2x USB 2.0, 2.5 GbE, 40-pin GPIO |
| **Availability & Price (PL)** | High availability; ~840–930 PLN (8 GB)                                     | Good availability; ~850–1000 PLN (8 GB)                                            | Moderate availability; ~1150–1220 PLN (8 GB)                                                    |

## Conclusion

All three candidates meet the core ARM architecture (**DEC-001**) and Linux GUI requirements, but they serve different priorities within the **1000–2000 PLN** project budget:

1. **Primary Recommendation for Fast & Reliable Prototyping (Best Ecosystem): Raspberry Pi 5 (8 GB)**
   - **Why:** Guarantees zero driver headaches for external Wi-Fi adapters, SDR receivers, touchscreen calibration, and GPIO/UART integration with the **Seeed Studio XIAO ESP32-C6**.
   - **Mitigation required:** Pair with a slim bottom-mounted NVMe Base (to avoid vertical HAT bulk) and use a 12V/15V/20V USB-C PD trigger + 5V/5A buck converter in `PCB-PWR` so any standard USB-C PD power bank can power the unit without triggering low-voltage warnings (**DEC-002**).

2. **Primary Recommendation for Performance-per-Watt & Compact NVMe: Orange Pi 5 Pro (8 GB)**
   - **Why:** The 8nm RK3588S SoC offers significantly better multi-core headroom and lower idle power draw for future battery operation, while keeping the compact Raspberry Pi mounting footprint and integrating onboard M.2 NVMe + Wi-Fi/BT without extra daughterboards.

3. **Best Feature-Rich / Field Admin Alternative: Radxa ROCK 5B (8 GB)**
   - **Why:** If enclosure volume allows the 100 x 72 mm Pico-ITX board and budget permits, native 9V–20V USB-C PD input, 2.5 GbE networking, full PCIe 3.0 x4 NVMe, and the built-in **HDMI Input** (for headless server troubleshooting) make it the ultimate hardware platform for a field diagnostic terminal.