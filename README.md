💧 AquaVision: An Accessible, Dual-Node IoT Monitoring System for Aquaponic Farms

This repository contains the complete design, code, and documentation for AquaVision, an Internet of Things (IoT) solution developed to provide real-time, remote monitoring of critical parameters (Temperature and Water Level) in small-scale aquaponic environments.

The project is specifically designed as Assistive Technology, enabling users with disabilities to manage and monitor their farms without the need for physical presence or complex visual analysis through the use of a Voice-Activated AI Chatbot and automated SMS alerts.

🌟 Key Features

Dual-Node Architecture: Uses two ESP32 devices (Center Node and Edge Node) for distributed monitoring and robust communication.

Decentralized Communication: Employs the ESP-NOW protocol for ultra-low power, low-latency communication between nodes in the farm.

Remote Connectivity: Utilizes a GSM Module (with optional Wi-Fi fallback) on the Edge Node/Gateway for reliable cloud connectivity, crucial for rural or remote deployment.

Accessibility Focus: Integrates with a MATLAB-based AI Chatbot (Initial Prototype) and a Web Dashboard (IoT-Enhanced Version) for natural language status queries and remote management.

Cloud Backend: Stores all real-time data securely in a Firebase Realtime Database.

Intelligent Alerting: Automated SMS and buzzer alerts for critical parameters like low water level.

⚙️ System Architecture (IoT-Enhanced Version)

The system operates on a Star-of-Stars topology, optimized for power efficiency and reliability.

1. Physical Layer (Nodes)

Component

Role

Function

Wireless Protocol

Center Node

Sensor Client

Measures water level ($\text{HC-SR04/VL53L0X}$) and temperature ($\text{DS18B20}$) in deep water. Battery-powered for mobility.

ESP-NOW (Client)

Edge Node

Gateway / Server

Receives data from the Center Node via ESP-NOW, aggregates local data, and forwards all information to the cloud. Wall-powered.

ESP-NOW (Server)

2. Network and Cloud Layer

Gateway-to-Cloud: $\text{GSM/GPRS (via SIM800L)}$ over $\text{HTTPS}$. This ensures connectivity even without local Wi-Fi.

Cloud Service: Firebase Realtime Database and Cloud Functions for data processing, authentication, and alert generation.

Software Protocol: Firebase REST API for low-overhead, secure data transmission.

🛠️ Project Evolution & Phases

The project was developed in two distinct phases to ensure functionality and scalability.

Phase 1: Proof-of-Concept (MATLAB Prototype)

Goal: Validate sensor accuracy and the AI Chatbot interface.

Components: Single ESP32 connected directly to a PC via Serial/USB.

Interface: MATLAB Desktop Application (GUI + AI Chatbot).

Limitation: Not a true IoT system (no wireless node communication or remote access).

Phase 2: IoT-Enhanced Deployment (Final System)

Goal: Achieve full remote monitoring and robust connectivity for real-world deployment.

Components: Dual ESP32 nodes, SIM800L GSM module.

Communication: ESP-NOW (Node-to-Node) and GSM (Gateway-to-Cloud).

Interface: Web Dashboard accessible via HTTPS.

Status: This is the version documented for the Final Report.

📂 Repository Structure (To be filled with code)

Directory

Content Description

01_Firmware_CenterNode

Arduino/C++ code for the battery-powered Center Node (ESP-NOW client).

02_Firmware_EdgeNode_Gateway

Arduino/C++ code for the Edge Node (ESP-NOW server, GSM/Firebase client).

03_MATLAB_AI_Chatbot

MATLAB scripts and GUI files for the Proof-of-Concept AI interface.

04_Web_Dashboard

HTML, CSS, and JavaScript for the Firebase-integrated web dashboard.

05_Hardware_Design

Fritzing diagrams, PCB layouts, and component datasheets.

Documentation

Final Report, Initial Report, and Presentation materials.

🤝 Group Members & Contact

[Yousef Khaled Omar Mahmoud] - Lead Engineer, Firmware & Hardware Integration

[Partner Name] - Cloud & Web Interface Development

Developed for ELC4015: Selected Topics in Communications: Internet of Things, Cairo University.
