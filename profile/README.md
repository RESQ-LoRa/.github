# DisasterChat
**Infrastructure-Independent Disaster Communication & Chat Application**
*Proposed Architecture by RESQ Organization*

## Project Status
This repository contains the system architecture, mathematical models, and implementation roadmap for DisasterChat. The project is currently in the design and simulation phase and has not yet been fully implemented into production code.

## Overview
[cite_start]DisasterChat is a proposed infrastructure-independent emergency communication network[cite: 6]. [cite_start]It is purpose-built for the critical 72-hour window following a major natural disaster, a period characterized by complete communications blackouts when cellular towers lose power and fiber cables are severed[cite: 6, 18, 19, 20]. [cite_start]The system aims to allow disaster survivors to send text messages, SOS alerts, GPS location pings, voice-to-text messages, and AI-generated visual reports to rescue teams without relying on base stations or the internet[cite: 7].

## Proposed System Architecture
[cite_start]The design organizes the network into a three-layer decentralized architecture[cite: 35]:

* [cite_start]**Layer 1 - Victim Side:** An Android application with a WhatsApp-style interface pairs via Bluetooth Low Energy to a low-cost LoRa Handheld Transceiver (HHT)[cite: 8, 37]. [cite_start]The HHT consists of an ESP32-S3 and an SX1262 LoRa module[cite: 37].
* [cite_start]**Layer 2 - Relay Nodes & Gateway:** Fixed relay nodes autonomously execute forwarding decisions using solar power and weather-proof enclosures[cite: 37]. [cite_start]A Gateway node bridges the LoRa mesh to the internet via an LTE modem when connectivity is available[cite: 37].
* [cite_start]**Layer 3 - Rescue Command Centre:** A web dashboard built with Flask and Leaflet.js running on a Raspberry Pi 4[cite: 37]. [cite_start]It is designed to display real-time survivor maps, an SOS triage queue, and scene reports[cite: 37].

## Planned Core Features
* [cite_start]**Multi-Modal Input:** The Android app will support typed text, speech-to-text via the Google Speech Recognition API, and image capture[cite: 9]. 
* [cite_start]**On-Device Image AI:** A MobileNetV3 model will run on the smartphone to generate a 60–80 byte text caption of disaster scenes, reducing bandwidth requirements by 1000x compared to raw image transmission[cite: 9, 31, 54].
* [cite_start]**Intelligent Geospatial Predictive Spray (IGPS) Routing:** The network backbone is designed to run the IGPS protocol, dynamically calculating the best next-hop for data packets[cite: 10].
* [cite_start]**TinyML Link Prediction:** A quantized Decision Tree model taking less than 1 KB of RAM is planned for the ESP32-S3 to forecast link degradation before it fails[cite: 10].
* [cite_start]**Pseudo-TDMA MAC Layer:** A scheduling layer will enforce strict SOS over Alert over Chat priority, ensuring critical life-saving packets are not queued behind routine traffic[cite: 11].

## Core Algorithms
The proposed routing and transmission mechanics rely on the following mathematical models:

**IGPS Routing Cost Function:**
[cite_start]The cost function to evaluate the optimal next-hop neighbour is defined as[cite: 100]:
[cite_start]$\Phi(i, j) = -w_1\cdot \text{Distance}(j,G) + w_2\cdot \text{SNR\_norm}(j) - w_3\cdot \text{Congestion}(j) + w_4\cdot S_{\text{pred}}(j) + w_5\cdot E_{\text{res}}(j)$ [cite: 100]

**Density-Adaptive Spray Limit:**
[cite_start]To prevent broadcast storms in dense networks, the spray limit ($L$) will dynamically adjust based on local node density[cite: 110]:
[cite_start]$L = \max(L_{\text{min}}, \min(L_{\text{max}}, \lceil \alpha \cdot D \cdot T_{\text{enc}} \rceil))$ [cite: 110]

## Implementation Roadmap
[cite_start]The project will be executed in five phases[cite: 140]:
1.  [cite_start]**Phase 1: Simulation & Design:** NS-3 100-node simulation, TinyML dataset generation, and hardware schematic design[cite: 143].
2.  [cite_start]**Phase 2: Hardware Prototype:** Breadboard assembly of the HHT and relay nodes, power bench testing, and LoRa range validation[cite: 143].
3.  [cite_start]**Phase 3: Firmware Development:** FreeRTOS task implementation, IGPS routing integration, and MAC scheduler development[cite: 143].
4.  [cite_start]**Phase 4: Android App Development:** Kotlin UI development, BLE GATT client integration, and MobileNetV3 TFLite implementation[cite: 143].
5.  [cite_start]**Phase 5: Integration & Evaluation:** Assembly of a 5-node physical prototype, end-to-end latency measurements, and PDR testing[cite: 143].

## Planned Repository Structure
[cite_start]As development commences, the repository will be structured as follows[cite: 131]:
* [cite_start]`/firmware`: PlatformIO build environment and C/C++ source code for ESP32-S3 devices[cite: 131].
* [cite_start]`/android`: Android application source code (Kotlin/Jetpack Compose)[cite: 93].
* [cite_start]`/sim`: NS-3 simulation scripts including topology models and routing headers[cite: 131].
* [cite_start]`/hardware`: KiCad schematics and hardware design files[cite: 143].
* [cite_start]`/dashboard`: Python backend and web interface for the Command Centre[cite: 97].

## Compliance & Standards
[cite_start]The completed project will target the following standards[cite: 138]:
* [cite_start]**Firmware:** MISRA C:2012 guidelines[cite: 136].
* [cite_start]**Radio:** India 865–867 MHz LoRa ISM Band regulations[cite: 138].
* [cite_start]**Hardware:** IEC 60529 IP65 enclosure ratings for relay nodes[cite: 138].
