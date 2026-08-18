<img src="https://github.com/user-attachments/assets/47d51a3d-a075-440f-b9df-2e13a8659e65" width="100" align="right">

# PIXPAPER-213-M
### 2.13" Mono / 4-Grayscale Electronic Paper Display Module

<div align="center">

![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![Platform](https://img.shields.io/badge/platform-ARM%20%7C%20RISC--V-green.svg)
![License](https://img.shields.io/badge/license-GPLv2-orange.svg)
![Status](https://img.shields.io/badge/status-Production%20Ready-brightgreen.svg)

</div>

---

## 🎯 Product Overview

**Open-EP** introduces **PIXPAPER-213-M** - A 2.13 inch mono (4-grayscale) Electronic Paper Display module developed in collaboration with **Triangle Alien Studio**. This prototype showcases exceptional craftsmanship and superior hardware quality, featuring an SPI interface fully compatible with worldwide embedded devices.

Unlike the 4-color **PIXPAPER-213-C**, this module supports **partial update**, which makes it a good fit for frequently refreshed content such as clocks, meters and animated UI elements.

<table>
<tr>
<td width="35%">
<img src="https://github.com/user-attachments/assets/e35bbb1c-74f1-4aef-a801-44871fa01ad4" width="100%">
</td>
<td width="65%">

### 📊 Technical Specifications

| Specification | Details |
|:-------------|:--------|
| **Screen Size** | 2.13 inch |
| **Resolution** | 250 × 122 pixels |
| **Color Support** | Black, White, 4 Grayscale |
| **PPI** | 130.6 |
| **Active Area** | 23.7046 × 48.55 mm |
| **Interface** | SPI |
| **Partial Update** | Supported |
| **Enclosure** | Plastic (3D printed) |
| **Operating Temp** | 0 - 40°C |

</td>
</tr>
</table>

### 🔌 Pin Configuration
```
3.3V | GND | MOSI | SCK | CS# | DC# | RST# | BUSY
```
> **Note:** DC#, RST#, and BUSY are GPIO-controlled

---

## 📚 Implementation Guide

Choose your implementation approach based on your application requirements:

<div align="center">

```mermaid
graph LR
    A[PIXPAPER-213-M] --> B[User-Space Applications]
    A --> C[Linux Kernel DRM]
    A --> D[Special Applications]

    B --> B1[Quick Start]
    B --> B2[Flexible Control]

    C --> C1[Hardware Acceleration]
    C --> C2[System Integration]

    D --> D3[Custom Solutions]
    D --> D4[Advanced Features]

    style A fill:#ff6b6b
    style B fill:#4ecdc4
    style C fill:#45b7d1
    style D fill:#ffd93d
```

</div>

---

## 🚀 User-Space Applications

> **Best for:** Rapid prototyping, application-level control, and cross-platform development

User-space drivers provide direct application control without kernel modifications. Ideal for quick deployment and testing across multiple platforms.

### 🖥️ MPU Platforms (ARM64)

<table>
<tr>
<td align="center" width="25%">

<a href="https://www.renesas.com/" target="_blank">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Renesas_Electronics_logo.svg/330px-Renesas_Electronics_logo.svg.png" height="80">
</a>

#### Renesas
**Status:** ✅ Ready

</td>
<td align="center" width="25%">

<a href="https://www.nxp.com/" target="_blank">
<img src="https://github.com/TechNexion-Vision/.github/assets/28101204/67cc61c0-6bb7-44d5-889a-1ba5d4c0b9b5" height="80">
</a>

#### NXP
**Status:** ✅ Ready

</td>
<td align="center" width="25%">

<a href="https://www.telechips.com/" target="_blank">
<img src="https://github.com/user-attachments/assets/4f260b12-4d99-42e3-b9bd-6b90b2bbec16" height="80">
</a>

#### Telechips
**Status:** ✅ Ready

</td>
<td align="center" width="25%">

<a href="https://www.raspberrypi.com/" target="_blank">
<img src="https://github.com/user-attachments/assets/f2c7c418-baf4-456f-81cd-1149b3247a4e" height="80">
</a>

#### Raspberry Pi
**Status:** ✅ Ready

</td>
</tr>
</table>

#### 📖 Supported Boards & Guides

| Manufacturer | Board / SoC | Porting Guide | Status |
|:------------|:-----------|:--------------|:------:|
| **Renesas** | KAKIP SBC (RZ/V2H) | [📄 Guide](https://github.com/open-ep/PIXPAPER-213-M/blob/main/KAKIP_PIXPAPAER-213-M.md) | ✅ |
| **NXP** | FRDM-IMX93 (IMX93) | [📄 Guide](https://github.com/open-ep/PIXPAPER-213-M/blob/main/FRDM-IMX93_PIXPAPAER-213-M.md) | ✅ |
| **Telechips** | TOPST D3-G (Dolphin 3M) | [📄 Guide](https://github.com/open-ep/PIXPAPER-213-M/blob/main/D3-G_PIXPAPAER-213-M.md) | ✅ |
| **Raspberry Pi** | Raspberry Pi 5 | [💻 Example](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-test-rpi5.c) (guide coming soon) | ✅ |

#### 🎬 Reference Examples

| Example | Description | Boards |
|:--------|:------------|:-------|
| **Basic update** | Full-screen mono / fast / 4-grayscale refresh from a PNG-converted header | [FRDM-IMX93](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-test-frdm-imx93.c) · [TOPST D3-G](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-test-topst-d3-g.c) · [Raspberry Pi 5](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-test-rpi5.c) |
| **Robot eye** | Animated demo driven by partial update | [KAKIP](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-robot-eye-kakip.c) · [FRDM-IMX93](https://github.com/open-ep/linux-user-space-examples/blob/master/2.13/mono/spi/pixpaper-213-m-robot-eye-frdm-imx93.c) |

### 🔧 MCU Platforms (RISC-V)

<table>
<tr>
<td align="center" width="25%">

<a href="https://www.uiap.jp/en/" target="_blank">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/RISC-V-logo-square.svg/1280px-RISC-V-logo-square.svg.png" height="80">
</a>

#### UIAP
**Status:** ✅ Ready

</td>
</tr>
</table>

| Manufacturer | Board / Core | Porting Guide | Status |
|:------------|:------------|:--------------|:------:|
| **UIAP** | UIAPduino Pro Micro (CH32V003) | [📄 Guide](https://github.com/open-ep/PIXPAPER-213-M/blob/main/UIAP-CH32V003_PIXPAPAER-213-M.md) | ✅ |

---

## 🐧 Linux Kernel DRM Integration

> **Best for:** System-level integration, hardware acceleration, and production deployments

DRM (Direct Rendering Manager) integration provides native Linux kernel support for optimal performance and seamless system integration.

### ✨ Advantages

<table>
<tr>
<td width="33%" align="center">

### ⚡ Performance
Hardware-accelerated rendering with zero-copy operations

</td>
<td width="33%" align="center">

### 🔄 Integration
Native support in framebuffer and display subsystems

</td>
<td width="33%" align="center">

### 🛡️ Stability
Kernel-space reliability with proper error handling

</td>
</tr>
</table>

### 📋 Platform Support Status

| Platform | Board | Architecture | DRM Driver Status | Kernel type |
|:---------|:------|:-------------|:------------------|:------------|
| **IMX93** | FRDM-IMX93 | ARM64 | 📝 Planned | Vendor Kernel 6.12↑ |
| **RZ/V2H** | KAKIP | ARM64 | 📝 Planned | Vendor Kernel 5.10 |
| **Dolphin 3M** | TOPST D3-G | ARM64 | 📝 Planned | TBD |
| **Raspberry Pi** | PI 5 | ARM64 | 📝 Planned | TBD |

> **Note:** DRM drivers are currently under active development. Contact us for early access programs.

---

## 🎨 Special Applications

> **Best for:** Custom solutions, research projects, and advanced use cases

Specialized implementations for unique requirements and cutting-edge applications.

### 🔬 Research & Development

<table>
<tr>
<td width="50%">

#### 🤖 Computer Vision
- Real-time image processing
- Low-power display output
- Edge AI integration

</td>
<td width="50%">

#### 📡 IoT Applications
- Battery-powered displays
- Remote monitoring systems
- Smart home dashboards

</td>
</tr>
<tr>
<td width="50%">

#### 🎓 Educational Projects
- Embedded systems learning
- Display technology research
- SPI protocol education

</td>
<td width="50%">

#### 🏭 Industrial Applications
- Process monitoring
- Equipment status displays
- Factory automation

</td>
</tr>
</table>

### 🛠️ Custom Development Services

We offer tailored solutions for your specific needs:

- ✅ Custom driver development
- ✅ Platform porting services
- ✅ Performance optimization
- ✅ Technical consulting
- ✅ Batch customization

### 📞 Contact for Special Projects

Have a unique application in mind? We'd love to collaborate!

---

## 🤝 Community & Support

<div align="center">

### Stay Connected

[![GitHub Issues](https://img.shields.io/badge/Issues-Report%20Bug-red.svg)](https://github.com/open-ep/PIXPAPER-213-M/issues)
[![GitHub Discussions](https://img.shields.io/badge/Discussions-Join%20Community-blue.svg)](https://github.com/open-ep/PIXPAPER-213-M/discussions)
[![Documentation](https://img.shields.io/badge/Docs-Wiki-green.svg)](https://github.com/open-ep/PIXPAPER-213-M/wiki)

</div>

### 📬 Get Help

- **Technical Issues:** [Open an Issue](https://github.com/open-ep/PIXPAPER-213-M/issues)
- **Feature Requests:** [Start a Discussion](https://github.com/open-ep/PIXPAPER-213-M/discussions)
- **Commercial Inquiries:** support@open-ep.org

---

## 📄 License & Credits

**PIXPAPER-213-M** is developed by **Open-EP** in collaboration with **Triangle Alien Studio**.

<div align="center">

Made with ❤️ for the Embedded Community

**[Documentation](https://github.com/open-ep/PIXPAPER-213-M/wiki)** • **[Examples](https://github.com/open-ep/linux-user-space-examples/tree/master/2.13/mono)** • **[Changelog](https://github.com/open-ep/PIXPAPER-213-M/blob/main/CHANGELOG.md)**

</div>
