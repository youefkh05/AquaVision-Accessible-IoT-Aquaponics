# Smart Parking IoT System

![Smart Parking IoT](https://raw.githubusercontent.com/youefkh05/Smart-Park-IoT-System/main/cover.png)

## Table of Contents
1. [Project Overview](#project-overview)  
2. [System Architecture](#system-architecture)  
3. [Hardware Components](#hardware-components)  
4. [Software Architecture](#software-architecture)  
5. [Data Communication](#data-communication)  
6. [Data Flow & Storage](#data-flow--storage)  
7. [Deployment & Prototype](#deployment--prototype)  
8. [References](#references)

## 📌 1. Project Overview

The **Smart Parking IoT System** is an end-to-end solution for real-time parking monitoring, occupancy detection, gateway aggregation, centralized control, and cloud-based access using scalable IoT infrastructure.  
The system integrates:

- ESP32-based parking slot nodes  
- Gate vehicle counting subsystem  
- Zone gateways for data aggregation  
- Central edge controller (dashboard & cloud sync)  
- Cloud backend for analytics, mobile API, and historical data

This repository provides **software implementation**, **hardware specifications**, and **architectural documentation** for the complete system.

GitHub Repo: https://github.com/youefkh05/Smart-Park-IoT-System

---

## 📌 2. System Architecture

The system follows a **three-tier IoT architecture**:

### **Perception Layer**
- Parking slot sensors (IR + ultrasonic)
- Vehicle presence detection

### **Aggregation Layer**
- Zone gateways aggregate multiple slot ESPs
- Wireless uplink (LoRa / sub-GHz) / Wi-Fi

### **Application Layer**
- Central node (edge controller with local dashboard)
- Cloud backend (MQTT Broker, storage, analytics)

**Figure 9.5 — System Architecture** illustrates the layered design.

---

## 📌 3. Hardware Components

### Table 10.1 — IR Parking Occupancy Sensor  
| Parameter | Specification |
|-----------|---------------|
| Sensor Type | Infrared Reflective Proximity |
| Model | TCRT5000 |
| Manufacturer | Vishay Semiconductors |
| Detection | IR + phototransistor |
| Range | 1–15 cm |
| Output | Digital / Analog |
| Role | Detect vehicle presence |

> Datasheet Reference: [16]

### Table 10.2 — Ultrasonic Distance Sensor  
| Parameter | Specification |
| Sensor Type | Ultrasonic Ranging Module |
| Model | HC-SR04 |
| Manufacturer | Generic |
| Range | 2 cm – 400 cm |
| Accuracy | ±1 cm |
| Interface | Trigger/Echo GPIO |
| Role | Redundancy for occupancy confirmation |

> Datasheet Reference: [17]

### Table 10.3 — Sensor Node Controller  
| Parameter | Specification |
| MCU | ESP32-WROOM-32 |
| Manufacturer | Espressif Systems |
| CPU | Dual-core Xtensa LX6 @ 240 MHz |
| RAM | 520 KB SRAM |
| Flash | 4 MB |
| Wireless | Wi-Fi & BLE |
| Voltage | 3.3 V |
| Role | Sensor control, data TX |

> Datasheet Reference: [18]

### Table 10.4 — Gateway Node Hardware  
| Parameter | Specification |
| Gateway | Raspberry Pi Zero W |
| Manufacturer | Raspberry Pi Ltd. |
| CPU | ARM1176JZF-S @ 1 GHz |
| RAM | 512 MB |
| Connectivity | Wi-Fi, USB Ethernet |
| OS | Raspberry Pi OS |
| Role | Zone aggregation & forwarding |

> Datasheet Reference: [19]

### Table 10.5 — Central Node Hardware  
| Parameter | Specification |
| Platform | Raspberry Pi 5 |
| Manufacturer | Raspberry Pi Ltd. |
| CPU | Quad-core ARM Cortex-A76 @ 2.4 GHz |
| RAM | 4 GB LPDDR4X |
| Storage | microSD / NVMe (PCIe) |
| Connectivity | Gigabit Ethernet, USB3.0 |
| Role | Dashboard, control, cloud sync |

> Datasheet Reference: [20]

---

## 📌 4. Software Architecture

Smart Parking software spans three layers:

### 4.1 Sensor Node Firmware
- **Platform:** ESP32 (Arduino / FreeRTOS)  
- **Language:** C/C++  
- Reads slot sensors and transmits occupancy data  
- Deep sleep for power efficiency

### 4.2 Gateway Software
- **Platform:** Raspberry Pi Zero W  
- **Language:** Python  
- MQTT subscriber, aggregator, publisher

### 4.3 Central Node & Cloud Services
- **Platform:** Raspberry Pi 5 (Flask / SQLite)  
- **Cloud:** AWS IoT Core + Lambda + RDS/S3  
- Web & mobile API

**Table 12 — Software Architecture** details layers and technologies.

> Software doc reference: [13]

---

## 📌 5. Data Communication

| Link | Protocol | Medium |
|------|----------|--------|
| Sensor → Gateway | LoRa / sub-GHz | Star (non-mesh) |
| Gateway → Central | TCP/IP over Ethernet | CAT6 |
| Central → Cloud | MQTT over TLS | 4G LTE / Broadband |

**Table 5 — MQTT Advantages**  
| Feature | Benefit |
| Publish/Subscribe | Scalable multi-client access |
| QoS 1 | Guaranteed delivery |
| Lightweight header | Ideal for low power |
| Persistent sessions | Buffered during outages |

> MQTT standard: [21]

---

## 📌 6. Data Flow & Storage

**Table 8 — System-Wide Data Flow & Storage** demonstrates volumes:
- ~2.6 MB/day total traffic
- ~78 MB/month
- ~396 MB/year cloud storage

**Figure 7.5 — System-Wide Data Flow & Storage** visually captures actual movement from physical sensors to cloud storage.

Cloud data references: [11]

---

## 📌 7. Deployment & Prototype

### 7.1 Gate Monitoring Subsystem  
**Figure 13.2 — Gate Monitoring Subsystem**  
- IR sensors trigger vehicle count
- Counter maintains park occupancy estimate

### 7.2 Slot Sensing Subsystem  
**Figure 13.3 — Slot-Level ESP Distribution**  
- One ESP per five slots
- Bitmask occupancy

### 7.3 Gateway Aggregation Subsystem  
**Figure 13.4 — Gateway Aggregation Logic**  
- Combines slot and gate data
- Determines parking availability

---

## 📌 References

```text
[11] Geng, Y., & Cassandras, C. G., “New ‘Smart Parking’ System Based on Resource Allocation…,” IEEE Trans. on ITS, Sep. 2013.

[13] Python Software Foundation; Raspberry Pi Ltd.; Meta Platforms, Inc.; SQLite Consortium, “Official Documentation for Raspberry Pi OS, Flask…,” 2018–2024.

[16] Vishay Semiconductors, “TCRT5000 Reflective Optical Sensor Datasheet,” Vishay Intertechnology, Inc., Mar. 2019.

[17] Robot Electronics Ltd., “HC-SR04 Ultrasonic Ranging Module Datasheet,” United Kingdom, 2018.

[18] Espressif Systems, “ESP32-WROOM-32 Datasheet,” Version 3.9, 2022.

[19] Raspberry Pi Ltd., “Raspberry Pi Zero W Product Brief,” Raspberry Pi Foundation, 2020.

[20] Raspberry Pi Ltd., “Raspberry Pi 5 Product Brief,” Raspberry Pi Foundation, Oct. 2023.

[21] OASIS Standard, “MQTT Version 3.1.1,” Oct. 2014.
