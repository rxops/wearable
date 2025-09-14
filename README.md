# Wearable Health Monitor IoT Device & SDK for Healthcare

The Wearable Health Monitor is a compact, low-power IoT platform for continuous vital sign acquisition (HR, SpO₂, skin temperature, HRV, activity) with early warning logic and secure data integration into healthcare or research systems. The companion SDK + reference API accelerates integration into clinical dashboards, remote patient monitoring (RPM) workflows, and wellness analytics pipelines.

## Table of Contents

- [Project Goals](#project-goals)
- [Problem/Solution/Impact](#problem-solution-impact)
- [Hardware Components & Sensor Roles](#hardware-components-and-sensor-roles)
- [Module Dimensions](#module-dimensions)
- [Possible Device Dimensions](#possible-device-dimensions)
- [Optional Features](#optional-features)
- [Data Collection](#data-collection)
- [System Architecture](#system-architecture)
- [Power & Energy Budget](#power--energy-budget)
- [System Integration](#system-integration)
- [Software Development Kit (SDK)](#software-development-kit-sdk)
- [API Reference (Draft)](#api-reference-draft)
- [Data Schema Examples](#data-schema-examples)
- [Security & Compliance](#security--compliance)
- [Applications](#applications)
- [Testing & Validation](#testing--validation)
- [Roadmap / Future Development](#future-development)
- [Contributing](#contributing)
- [License](#license)
- [Summary](#summary)

## Project Goals

The primary goal is to build a functional prototype of the wearable health monitor, focusing on a complete hardware architecture that integrates sensors effectively. The design emphasizes cost-effectiveness for easy adaptation in commercial healthcare environments, ensuring it can fit various needs without high expenses.

Key objectives:
- Develop a generic, adaptable hardware setup that works across different healthcare scenarios.
- Prioritize sensor roles and data accuracy for reliable monitoring.
- After prototyping, design and fabricate a custom PCB with SMD modules for optimized production and scalability.

This device helps users stay aware of their health daily, potentially preventing serious issues and reducing the need for frequent doctor visits. By focusing on affordability and ease of use, it empowers individuals and healthcare providers with timely, actionable health data.

## Problem/Solution/Impact

### Problem
Traditional health monitoring often relies on bulky, expensive devices that are not suitable for continuous, everyday use. Many people lack access to affordable tools for tracking vital signs like heart rate, oxygen levels, and temperature at home or on the go. This leads to delayed detection of health issues, higher healthcare costs, and limited ability for doctors to monitor patients remotely.

### Solution
Our wearable health monitor is a small, lightweight device that continuously tracks key health metrics using simple sensors. It connects wirelessly to phones or the internet, sending data securely to healthcare providers or apps. The device is easy to wear, powered by a long-lasting battery, and comes with a software kit that makes it simple for developers and healthcare systems to integrate the data.

### Impact
By providing affordable, continuous health monitoring, this device can help catch health problems early, reduce hospital visits, and improve patient care. It empowers individuals to take control of their health, supports remote patient monitoring for better outcomes, and lowers costs for healthcare systems. In the long term, it can contribute to better public health by enabling data-driven insights and preventive care.

## Hardware Components and Sensor Roles

The hardware architecture is designed for cost-effectiveness and adaptability, using standard, affordable components that can be easily sourced and integrated. This ensures the prototype is functional and scalable for commercial healthcare use. These choices keep the device lightweight and comfortable to wear all day, while providing reliable measurements.

### Microcontroller
* **Microcontroller: Seeed XIAO ESP32-C6** – A small computer chip that supports Wi-Fi and Bluetooth for wireless connections, designed to use very little power for continuous health monitoring.

  Key features:
  - Wi-Fi for sending data to the cloud periodically
  - Bluetooth for quick connection to phones or apps
  - Low-power modes for efficient battery use during monitoring

    <img width="auto" height="200" alt="image" src="assets/487221395-ad684b79-3f96-4360-80c6-31ebb8745015.png" />
    <img width="auto" height="200" alt="image" src="assets/XIAO-ESP32C6-4.png" />
    <img width="auto" height="200" alt="image" src="assets/F6EL5HNM3ZWC6J3.png" />

### Sensors
* **Pulse Oximeter & Heart Rate Sensor** (for example, Maxim MAX30102)
  - **Connection**: Standard communication method for data transfer
  - **Signals**: Light signals from red and infrared LEDs to measure blood flow, plus temperature
  - **Measurements**: Heart rate, blood oxygen level (SpO₂), blood flow quality, heart rate variability (HRV - variation in time between heartbeats)
  - **Notes**: Optimized LED brightness to save battery

    <img width="auto" height="200" alt="image" src="assets/487228208-28cd40a6-15fe-4358-bb83-1c2087b71c4a.png" />
    <img width="auto" height="200" alt="image" src="assets/487228916-00e2713d-bbf1-4c84-8683-0cc38eb209a7.png" />

* **Body Temperature Sensor** (for example, Melexis MLX90632)
  - **Connection**: Standard communication method
  - **Measurement**: Skin temperature, adjusted to estimate body core temperature
  - **Use**: Detecting fever, tracking daily temperature patterns, understanding changes in blood flow

* **Motion Sensor** (for example, Bosch BMI270) (planned)
  - **Connection**: Standard communication methods
  - **Measurement**: Movement in three directions; counts steps, detects position, helps filter out movement interference in heart rate measurements

* **Battery Monitor** (optional, for example, Maxim MAX17048)
  - **Measurement**: Battery charge level and voltage changes to adjust monitoring frequency

* **Optional Environmental (future)**: Humidity / ambient temp (SHTC3), barometric pressure (BMP390) for context data.

    <img width="auto" height="200" alt="image" src="assets/487226981-cddb6d25-80e5-4128-9f71-87d094b1067b.png" />
    <img width="auto" height="200" alt="image" src="assets/487227354-0505348d-5cc2-422d-a15f-0a94faac48a8.png" />

### Module Dimensions
* **ESP32-C6 Module**: Approximately 18mm x 25.5mm x 2.8mm, making it compact for integration into small wearable devices.
* **Pulse Oximeter and Heart Rate Sensor**: About 5.6mm x 3.3mm x 1.55mm, small enough to fit discreetly on the device.
* **Body Temperature Sensor**: Roughly 3mm x 3mm x 0.9mm, ultra-compact for precise placement.

### Possible Device Dimensions

The wearable device can be configured in different sizes for various use cases, balancing compactness with functionality.

| Configuration | Dimensions | Weight | Use Case |
|---------------|------------|--------|----------|
| Without Band - Compact | 30mm x 15mm x 8mm | - | Minimal, discreet monitoring in tight spaces or as a clip-on module |
| Without Band - Standard | 40mm x 20mm x 10mm | - | General wear, housing all components comfortably |
| With Band - Small | Main body 40mm x 20mm x 10mm + band 200mm x 25mm x 2mm | 25-30g | Adjustable arm band for everyday use |
| With Band - Large | Main body 50mm x 25mm x 12mm + band 250mm x 30mm x 2mm | 35-40g | For broader coverage or additional features |

These dimensions ensure cost-effective design, easy fabrication, and adaptability to different body sizes and healthcare scenarios.

  <img width="auto" height="200" alt="image" src="assets/diy-my-first-biceps-band-2-15-minutes-v0-1x0atzuwmita1.webp" />
  <img width="auto" height="200" alt="image" src="assets/il_fullxfull.7129883805_t9j4.webp" />

## Optional Features

### Display Integration
For future versions requiring visual output, a small round display can be integrated. The Seeed Studio Round Display for XIAO is a compatible option:

<img width="auto" height="200" alt="Seeed Studio Round Display" src="assets/rounddisplay.jpg" />
<img width="auto" height="200" alt="Seeed Studio Round Display Pinout" src="assets/round-pinout.png" />

- **Specifications**: 1.28-inch round capacitive touch screen, 240×240 resolution, 65K colors, 39mm diameter.
- **Features**: Onboard RTC, battery charging, TF card slot, suitable for wearable projects.
- **Compatibility**: Works with ESP32-C6 and other XIAO modules for plug-and-play setup.
- **Setup Guide**: Refer to the [Seeed Studio getting started guide](https://wiki.seeedstudio.com/get_start_round_display/) for hardware preparation, software installation, and example demos.

This optional display enhances user interaction while maintaining the device's focus on sensor-based monitoring.

### Data Collection
Continuous or adaptive sampling of HR / SpO₂ / temperature with motion-informed filtering. HRV derived from cleaned inter-beat intervals (time-domain: RMSSD, SDNN; frequency-domain optional in host/cloud). Activity classification initially basic (rest / active) using accelerometer magnitude variance.

This smart sampling ensures the device captures important health changes without overwhelming the user with too much data.

Sampling strategy (baseline):
| Signal | Raw Sample Rate | Processing Window | Output Interval |
|--------|-----------------|-------------------|-----------------|
| PPG (IR/Red) | 50–100 Hz | 5–8 s sliding | 5 s HR / SpO₂ |
| Skin Temp | 0.2–1 Hz | 60 s median | 60 s |
| Motion Accel | 25–50 Hz | 4 s | 4–10 s activity state |
| Battery | 0.016 Hz (1/min) | N/A | 60 s |

Adaptive downscaling when stable (e.g., night mode) to save energy.

Artifacts filtered using: band-pass (0.5–5 Hz PPG), motion-correlated segment rejection, interpolation of short gaps.

## System Architecture

High-level data flow:

```
[Sensors: PPG | Temp | IMU] --I2C/SPI--> [MCU Acquisition Layer]
  -> Ring Buffers -> [Signal Conditioning & Feature Extraction]
  -> Metric Cache -> [Edge Alerts Engine]
  -> BLE (GATT) <-> Phone App (real-time)
  -> Wi-Fi Batch Uploader -> [Secure API Gateway]
              |
           [Message Queue]
              |
            [Processing / Normalization]
              |
             [FHIR Mapper + Storage]
              |
           [Analytics / Dashboard / EHR]
```

Edge Alerts Engine (examples):
- Low SpO₂ sustained (< 92% for > 30 s)
- Tachycardia / Bradycardia thresholds age-configurable
- Rapid temp rise (>0.8°C over 15 min)
- High motion artifact suppression (flag data quality)

## Power & Energy Budget

Indicative (prototype, 3.7V Li-Po 150–200 mAh):

| Subsystem | Active (mA) | Duty Cycle | Avg (mA) Notes |
|-----------|-------------|------------|----------------|
| MCU (light sleep baseline) | 3.0 | 70% | 2.1 |
| Wi-Fi burst sync | 120 | 1% | 1.2 (short transfers) |
| BLE advertising/conn | 8 | 20% | 1.6 (interval tuned) |
| PPG Sensor LEDs + AFE | 6–12 | 50% adaptive | 4.5 median |
| Temp Sensor | 1 | 5% | 0.05 |
| IMU | 0.8 | 30% | 0.24 (ODR reduced) |
| Power Regulation Loss | - | - | 0.4 overhead |
| Total Est. Avg | - | - | ~10.1 mA |

Estimated runtime (150 mAh / 10.1 mA) ≈ 14–15 h (continuous). Target optimization path:
- Night / rest mode: reduce PPG (LED current + sample rate) → 30–40% savings
- Opportunistic Wi-Fi batching (every 10–30 min)
- Motion-aware HR sampling backoff when stable

Goal: 24 h with 200 mAh cell after optimizations.

## System Integration

To build an effective wearable system, components must work together smoothly for data flow and communication:

* **Sensor Connection**: Sensors link to the microcontroller using standard interfaces, enabling coordinated data gathering. The processor converts raw data into useful health metrics.
* **Wireless Features**: Includes Bluetooth and Wi-Fi for short-range and internet-based data transfer. Bluetooth connects to nearby devices like phones, while Wi-Fi allows direct cloud uploads.
* **Power Efficiency**: Optimized energy use keeps the device running longer on battery power, with smart modes for continuous monitoring.
* **Data Processing**: The microcontroller combines inputs from sensors into organized data packets for reliable transmission.
* **Network Expansion**: For multiple devices, wearables can connect in networks or through hubs that relay data to cloud services or healthcare platforms.

This setup creates reliable data pathways from the device to user applications.

### Integration with Healthcare Platforms
The wearable can be integrated as part of broader healthcare ecosystems like MyDR24, providing patients and providers with real-time, streamlined medical data. This enables seamless care coordination, telemedicine, and proactive health management within a comprehensive digital health platform.

## Software Development Kit (SDK)

The project includes an SDK for easy integration with other systems:

* **APIs**: REST + WebSocket streaming for real-time metrics, pagination for historical queries.
* **Data Formats**: JSON, optional HL7 FHIR resources (Observation, Device, Patient) via mapper.
* **Security**: OAuth2 (client credentials / device code), JWT access tokens, TLS 1.2+.
* **Edge → Cloud Sync Modes**: Real-time BLE relay; deferred Wi-Fi batch (compressed JSON lines); push via MQTT (optional future).
* **Client Libraries**: Planned: JavaScript/TypeScript, Python, Go. Provide typed models + retry/backoff.
* **Alert Customization**: Threshold + trend-based rules definable via /alerts endpoints.
* **Data Quality Flags**: Motion artifact %, IR signal quality index, perfusion index.

## API Reference (Draft)

Base URL (example): `https://api.examplehealth.dev/v1`

Authentication: `Authorization: Bearer <token>`

| Method | Path | Purpose |
|--------|------|---------|
| POST | /auth/device/register | Provision a device (returns credentials) |
| POST | /auth/token | OAuth2 token exchange |
| GET | /devices/{id} | Device metadata |
| GET | /devices/{id}/metrics/latest | Latest composite vitals |
| GET | /devices/{id}/metrics/stream (WS) | Live streaming (JSON frames) |
| GET | /devices/{id}/metrics?from=..&to=.. | Historical time-series |
| GET | /devices/{id}/alerts | Active + past alerts |
| POST | /alerts/rules | Create alert rule |
| GET | /fhir/Observation?device=... | FHIR Observations (server mapped) |

Example: Latest Metrics Response
```json
{
  "deviceId": "dev_12345",
  "timestamp": "2025-09-12T08:15:27Z",
  "hr": 72,
  "spo2": 97,
  "hrv": { "rmssd": 41 },
  "skinTempC": 33.4,
  "activity": "rest",
  "batteryPct": 84,
  "quality": { "ppgMotionFlag": false, "perfusionIndex": 5.2 }
}
```

WebSocket Frame (example):
```json
{"t":"2025-09-12T08:15:28.500Z","hr":72,"spo2":97,"motion":0.02}
```

## Data Schema Examples

### Internal Edge Packet (compressed JSON lines pre-upload)
```json
{
  "t": "2025-09-12T08:15:20Z",
  "hr": 72,
  "spo2": 97,
  "st": 33.4,
  "b": 3.98,
  "act": 0,
  "q": { "af": 0.01, "pi": 5.2 }
}
```

### FHIR Observation (HR example)
```json
{
  "resourceType": "Observation",
  "status": "final",
  "category": [{"coding":[{"system":"http://terminology.hl7.org/CodeSystem/observation-category","code":"vital-signs"}]}],
  "code": {"coding":[{"system":"http://loinc.org","code":"8867-4","display":"Heart rate"}]},
  "subject": {"reference": "Patient/pat_001"},
  "device": {"reference": "Device/dev_12345"},
  "effectiveDateTime": "2025-09-12T08:15:27Z",
  "valueQuantity": {"value": 72, "unit": "beats/min", "system": "http://unitsofmeasure.org", "code": "/min"}
}
```

## Security & Compliance

| Aspect | Approach |
|--------|---------|
| Transport | TLS 1.2+ enforced; certificate pinning optional in mobile SDK |
| Data at Rest | Encrypted storage (AES-256) for cached packets on device & server DB encryption |
| AuthN/Z | OAuth2 + scoped JWT; per-device key rotation |
| PII Separation | Device telemetry decoupled from patient identity (link table w/ access controls) |
| Audit | Immutable append-only audit log for data access & alert modifications |
| Regulatory Considerations | HIPAA (US), GDPR (EU) principles (minimization, consent, deletion workflow) |
| Secure Boot / Firmware | Signed firmware images (future) + version attestation |

Threat Surface Mitigations:
- Replay prevention: nonce + timestamp in batch envelope
- BLE pairing with passkey or numeric comparison
- Rate limiting / anomaly detection for API keys

## Applications

The SDK helps build connected health solutions.

## Applications

The wearable supports various health needs by using collected data for monitoring and alerts:

### Managing Chronic Conditions
- Tracks vital signs for long-term illnesses, enabling early interventions and reducing hospital visits.

### Home-Based Care
- Monitors recovery at home, providing real-time data for virtual check-ups and timely alerts.

### Senior Care
- Detects falls and vital sign changes in elderly settings, ensuring quick responses.

### Medical Research
- Collects objective data for clinical studies, helping evaluate treatments.

### Remote Healthcare
- Shares data with doctors during virtual visits for better diagnosis and care planning.

These uses highlight the device's role in preventive and specialized care.

## Testing & Validation

| Layer | Method |
|-------|--------|
| Sensor Signal | Controlled bench tests with optical tissue simulators / temp plates |
| Algorithm | Synthetic waveform injection + golden HR/SpO₂ traces |
| Firmware | Unit tests (filter windows, HRV calc), power profiling scripts |
| Cloud API | Contract tests (OpenAPI), load tests for streaming sessions |
| Data Quality | Compare against clinical-grade reference (pulse oximeter, thermometer) |

Calibration Strategy:
- Initial LED current sweep per user during pairing
- Temperature offset calibration vs ambient + skin contact settling (first 3–5 min)
- Motion artifact model refinement with labeled activity sessions

Quality Metrics: Missing sample %, artifact rejection rate, drift vs reference, uptime.

## Future Development

Once the prototype is complete, the next steps include:
- Designing and fabricating a custom PCB with integrated SMD modules for improved efficiency and reduced costs.
- Expanding the SDK with more features for broader healthcare integrations.
- Testing in real-world clinical settings for validation and refinements.
- Exploring partnerships for commercial production and distribution.

Contributions and feedback are welcome to advance this project.

## Contributing

We welcome contributions! Suggested first steps:
1. Open an issue describing feature/bug (use labels: `enhancement`, `firmware`, `sdk`, `documentation`).
2. Discuss design (attach sequence or state diagrams if architectural).
3. Fork & create a feature branch: `feature/<short-description>`.
4. Provide tests / sample data where applicable.
5. Submit PR referencing issue; fill checklist (lint passes, docs updated, no secrets committed).

Future addition: a dedicated `CONTRIBUTING.md` with coding standards, OpenAPI contribution steps, and firmware build instructions.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Summary

An extensible wearable health telemetry platform emphasizing low-cost sensing, secure data pathways, and interoperable health data (FHIR-ready). Designed for integration with digital health ecosystems like MyDR24 to provide real-time medical insights. This README now outlines hardware component options, architecture, energy model, preliminary API, data schemas, and compliance posture to accelerate prototype-to-product evolution.

---

Status: Early prototype phase. Contributions and feedback encouraged.
