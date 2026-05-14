# iMX6 Rex Module — Custom 12-Layer PCB Design

![PCB Front](iMX6%20Rex_V1I1_PCB.png)

> A custom **12-layer PCB layout** for the **iMX6 Rex System-on-Module (SoM)**, based on the open-source schematic released by **FEDEVEL Academy** under Creative Commons (CC BY-NC 4.0). The PCB was **designed entirely from scratch by me** as a hands-on hardware design learning project.

---

## 📌 Project Overview

The **iMX6 Rex Module** is a well-known open-source hardware project originally created by [FEDEVEL Academy](https://www.fedevel.com/academy/) and published at [imx6rex.com](https://www.imx6rex.com/). It is built around the **NXP (Freescale) i.MX6 application processor** and is widely used as a teaching reference for advanced schematic and PCB design.

### What I did

- ✅ **Used the open-source schematic** released by FEDEVEL/iMX6 Rex as the electrical reference
- ✅ **Designed the PCB layout from scratch** — no existing PCB files were used
- ✅ Defined the **12-layer stackup** myself based on signal integrity requirements
- ✅ Performed **component placement, routing, length matching, and impedance control** independently
- ✅ Routed DDR3, high-speed differential pairs (HDMI, LVDS, PCIe, SATA, Ethernet, USB) by hand

> ⚠️ **Note:** This project is purely for learning and demonstration purposes. The original schematic is the work of FEDEVEL Academy and is licensed under [Creative Commons BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) (non-commercial). All credit for the electrical design goes to them.

---

## 🖼️ PCB Renders

### 3D Render — Front (Top side)
![PCB Front Render](iMX6%20Rex_V1I1_PCB.png)

### 3D Render — Back (Bottom side)
![PCB Back Render](iMX6%20Rex_V1I1_PCB_B.png)

---

## 🧩 iMX6 Rex Module — Specifications

Based on the official iMX6 Rex Module specification from [imx6rex.com](https://www.imx6rex.com/):

| Feature | Specification |
|---------|---------------|
| **CPU** | NXP (Freescale) i.MX6 processor, up to **1.2 GHz / 4 cores** |
| **Memory** | Soldered-down **DDR3-1066 (533 MHz)**, up to **4 GB** |
| **Ethernet** | 10 / 100 / 1000 Mbps |
| **Video Out** | 1× HDMI (up to QXGA 2048 × 1536), 1× LVDS |
| **High-speed** | 1× PCIe, 1× SATA, 2× USB |
| **Storage** | On-board SPI Flash up to 32 Mb; 1× SD (or 2× CAN); 1× MMC |
| **Serial I/O** | 3× UART, 3× I²C, 1× SPI |
| **Audio** | Digital audio |
| **Debug** | JTAG |
| **LEDs** | User LED, Power LED |
| **Connectors** | 2× high-speed board-to-board (J1 / J2) |
| **Board Size** | 70 × 40 mm (smaller than a credit card) |
| **Input Power** | 7 to 24 V DC (or single +5 V with mods) |

---

## 📐 My PCB Implementation

| Parameter | Value |
|-----------|-------|
| **Layers** | 12 |
| **Board Dimensions** | 70 × 40 mm |
| **EDA Tool** | Altium Designer |
| **Routing Style** | Controlled impedance, length-matched differential pairs |
| **Mounting Holes** | 4× GND-connected mounting points (corner) |
| **Connectors** | J1, J2 — high-density board-to-board |
| **Surface Finish** | ENIG (recommended) |

---

## 🔧 Layer Stackup

The 12-layer stackup I defined provides excellent power distribution and signal integrity for the high-speed DDR3 and differential pair routing.

| Layer | Function |
|-------|----------|
| **L1** | Signal — Top copper, component placement & fine routing |
| **L2** | Ground plane |
| **L3** | Signal — High-speed & DDR routing |
| **L4** | Ground plane |
| **L5** | Power plane |
| **L6** | Power plane |
| **L7** | Power plane |
| **L8** | Power plane |
| **L9** | Ground plane |
| **L10** | Signal — DDR & high-speed routing |
| **L11** | Ground plane |
| **L12** | Signal — Bottom copper, passive components |

**Stackup summary:** `Signal / GND / Signal / GND / Power×4 / GND / Signal / GND / Signal`

This stackup has **4 dedicated power layers** sandwiched between ground planes, providing a very low-impedance power distribution network — critical for the multiple voltage rails (1V375, 1V5, 2V5, 3V3) feeding the i.MX6 CPU, DDR3 memory, and peripheral logic.

---

## 🖼️ Layer-by-Layer PCB Views

| Layer | Preview |
|-------|---------|
| **L1 — Top Signal** | ![L1](L_1.png) |
| **L2 — Ground** | ![L2](L_2.png) |
| **L3 — Signal** | ![L3](L_3.png) |
| **L4 — Ground** | ![L4](L_4.png) |
| **L5 — Power** | ![L5](L_5.png) |
| **L6 — Power** | ![L6](L_6.png) |
| **L7 — Power** | ![L7](L_7.png) |
| **L8 — Power** | ![L8](L_8.png) |
| **L9 — Ground** | ![L9](L_9.png) |
| **L10 — Signal** | ![L10](L_10.png) |
| **L11 — Ground** | ![L11](L_11.png) |
| **L12 — Bottom Signal** | ![L12](L_12.png) |

---

## 🛠️ Design Process

1. **Schematic Reference** — Downloaded the official open-source iMX6 Rex schematic from [imx6rex.com](https://www.imx6rex.com/)
2. **Netlist Import** — Imported into Altium Designer and prepared the design environment
3. **Stackup Definition** — Designed a 12-layer impedance-controlled stackup (50 Ω single-ended, 90 Ω / 100 Ω differential)
4. **Component Placement**
   - i.MX6 BGA centered on the board
   - DDR3 memory ICs placed close to the CPU for short trace lengths
   - PMIC and switching regulators grouped on the periphery
   - Crystal oscillators (32.768 kHz and 25 MHz) placed near the CPU/PHY
5. **Power Routing** — Multi-rail power planes with adequate decoupling capacitors per the reference design
6. **High-Speed Routing**
   - DDR3: length-matched, impedance-controlled, properly fly-by topology
   - Differential pairs: HDMI, LVDS, PCIe, SATA, USB, Gigabit Ethernet — all routed with controlled impedance
7. **BGA Fanout** — Via-in-pad and tight escape patterns used to break out the i.MX6 BGA
8. **DRC & Signal Integrity Review** — Design rules verified; clearance, impedance and timing checked

---

## 📁 Repository Structure

```
iMX6-Rex-PCB/
├── README.md
├── iMX6 Rex_V1I1_PCB.png       # 3D render — front (top)
├── iMX6 Rex_V1I1_PCB_B.png     # 3D render — back (bottom)
├── L_1.png                      # Layer 1  — Signal (Top)
├── L_2.png                      # Layer 2  — Ground
├── L_3.png                      # Layer 3  — Signal
├── L_4.png                      # Layer 4  — Ground
├── L_5.png                      # Layer 5  — Power
├── L_6.png                      # Layer 6  — Power
├── L_7.png                      # Layer 7  — Power
├── L_8.png                      # Layer 8  — Power
├── L_9.png                      # Layer 9  — Ground
├── L_10.png                     # Layer 10 — Signal
├── L_11.png                     # Layer 11 — Ground
└── L_12.png                     # Layer 12 — Signal (Bottom)
```

---

## 🎓 What I Learned

This project gave me hands-on experience with:

- **Advanced multi-layer PCB stackup design** for high-speed digital systems
- **BGA fanout and escape routing** for high-pin-count processors
- **DDR3 routing rules** — fly-by topology, length matching, termination, impedance control
- **High-speed differential pair routing** — HDMI, LVDS, PCIe, SATA, USB, Gigabit Ethernet
- **Power distribution network (PDN) design** with multiple voltage rails and decoupling strategy
- **Crystal oscillator and clock signal placement** for low EMI
- **Working with open-source hardware** and giving proper credit to original creators

---

## 📜 Credits & Open Source Acknowledgement

### Original Schematic
- **Project:** [iMX6 Rex Module](https://www.imx6rex.com/)
- **Designed by:** [FEDEVEL Academy](https://www.fedevel.com/academy/)
- **License:** [Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

[![CC BY-NC 4.0](https://i.creativecommons.org/l/by-nc/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc/4.0/)

### PCB Layout
- **Designed by:** Tharinda (this repository)
- **Tool used:** Altium Designer
- **Status:** Educational / personal learning project

I want to give **full credit to FEDEVEL Academy** for releasing this excellent reference design as open source — it's an invaluable resource for anyone learning advanced PCB design. The original schematic, BOM, and reference documents are all available at [imx6rex.com](https://www.imx6rex.com/).

---

## 📄 License

The original iMX6 Rex schematic is licensed under **CC BY-NC 4.0** by FEDEVEL Academy and remains the intellectual property of the original authors.

The PCB layout in this repository is my own original work, created from scratch using the open-source schematic as electrical reference. It is shared here for **educational and personal use only**, in keeping with the non-commercial spirit of the original license.

---

## 🔗 Useful Links

- 🌐 [iMX6 Rex Official Website](https://www.imx6rex.com/)

---

