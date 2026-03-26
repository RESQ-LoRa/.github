# DisasterChat
**Infrastructure-Independent Disaster Communication & Chat Application**
*Proposed Architecture by RESQ Organization*

## Project Status
This repository contains the system architecture, mathematical models, and implementation roadmap for DisasterChat. The project is currently in the design and simulation phase and has not yet been implemented into production code.

## Overview
DisasterChat is a proposed infrastructure-independent emergency communication network. It is purpose-built for the critical 72-hour window following a major natural disaster, a period characterized by complete communications blackouts when cellular towers lose power and fiber cables are severed. The system is designed to allow disaster survivors to send text messages, SOS alerts, GPS location pings, voice-to-text messages, and AI-generated visual reports to rescue teams without relying on base stations or the internet.

## Proposed System Architecture
The design organizes the network into a three-layer decentralized architecture:

* **Layer 1 - Victim Side:** An Android application with a messaging interface pairs via Bluetooth Low Energy to a low-cost LoRa Handheld Transceiver (HHT). The HHT consists of an ESP32-S3 and an SX1262 LoRa module.
* **Layer 2 - Relay Nodes & Gateway:** Fixed relay nodes autonomously execute forwarding decisions using solar power and weather-proof enclosures, deliberately omitting camera modules to reduce cost and power consumption. A Gateway node bridges the LoRa mesh to the internet via an LTE modem when connectivity is available.
* **Layer 3 - Rescue Command Centre:** A web dashboard built with Flask and Leaflet.js running on a Raspberry Pi 4. It is designed to display real-time survivor maps, an SOS triage queue, and scene reports.

## Planned Core Features
* **Multi-Modal Input:** The Android app will support typed text, speech-to-text via the Google Speech Recognition API, and image capture. 
* **On-Device Image AI:** A MobileNetV3 model will run on the smartphone to generate a 60–80 byte text caption of disaster scenes, reducing bandwidth requirements by 1000x compared to raw image transmission.
* **Intelligent Geospatial Predictive Spray (IGPS) Routing:** The network backbone is designed to run the IGPS protocol, dynamically calculating the best next-hop for data packets.
* **TinyML Link Prediction:** A quantized Decision Tree model taking less than 1 KB of RAM is planned for the ESP32-S3 to forecast link degradation before failure.
* **Pseudo-TDMA MAC Layer:** A scheduling layer will enforce strict SOS > Alert > Chat priority, ensuring critical life-saving packets are not queued behind routine traffic.

## Core Algorithms
The proposed routing and transmission mechanics rely on the following mathematical models:

**IGPS Routing Cost Function:**
The cost function to evaluate the optimal next-hop neighbor is defined as:
$\Phi(i, j) = -w_1 \cdot \text{Distance}(j,G) + w_2 \cdot \text{SNR\_norm}(j) - w_3 \cdot \text{Congestion}(j) + w_4 \cdot S_{\text{pred}}(j) + w_5 \cdot E_{\text{res}}(j)$

**Density-Adaptive Spray Limit:**
To prevent broadcast storms in dense networks, the spray limit ($L$) will dynamically adjust based on local node density:
$L = \max(L_{\text{min}}, \min(L_{\text{max}}, \lceil \alpha \cdot D \cdot T_{\text{enc}} \rceil))$

## Implementation Roadmap
The project will be executed in five phases:
1. **Phase 1: Simulation & Design:** NS-3 100-node simulation, TinyML dataset generation, and hardware schematic design.
2. **Phase 2: Hardware Prototype:** Breadboard assembly of the HHT and relay nodes, power bench testing, and LoRa range validation.
3. **Phase 3: Firmware Development:** FreeRTOS task implementation, IGPS routing integration, and MAC scheduler development.
4. **Phase 4: Android App Development:** Kotlin UI development, BLE GATT client integration, and MobileNetV3 TFLite implementation.
5. **Phase 5: Integration & Evaluation:** Assembly of a 5-node physical prototype, end-to-end latency measurements, and packet delivery rate testing.

## Planned Repository Structure
As development commences, the repository will be structured as follows:
* `/firmware`: PlatformIO build environment and C/C++ source code for ESP32-S3 devices.
* `/android`: Android application source code targeting Kotlin and Jetpack Compose.
* `/sim`: NS-3 simulation scripts including topology models and routing headers.
* `/hardware`: KiCad schematics and hardware design files.
* `/dashboard`: Python backend and web interface for the Command Centre.

## Hardware, Software & Frameworks
* **Hardware:** ESP32-S3, SX1262 LoRa Radio, Raspberry Pi 4.
* **Software/Frameworks:** FreeRTOS, NS-3, Kotlin, Jetpack Compose, TensorFlow Lite (MobileNetV3), PlatformIO, Python (Flask), KiCad. 

## Compliance & Standards
The completed project will target the following standards:
* **Firmware:** MISRA C:2012 guidelines.
* **Radio:** India 865–867 MHz LoRa ISM Band regulations.
* **Hardware:** IEC 60529 IP65 enclosure ratings for relay nodes.
