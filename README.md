# Wearable Health Monitor IoT Device and SDK for Healthcare

Introducing the Wearable Health Monitor: a compact IoT device designed to revolutionize healthcare by continuously tracking vital signs, delivering early health alerts, and enabling remote consultations. Paired with our comprehensive SDK, it seamlessly integrates with healthcare systems for enhanced patient care in chronic management, home-based recovery, and wellness monitoring.

## Table of Contents

- [Project Goals](#project-goals)
- [Hardware Components and Sensor Roles](#hardware-components-and-sensor-roles)
- [Module Dimensions](#module-dimensions)
- [Possible Device Dimensions](#possible-device-dimensions)
- [Optional Features](#optional-features)
- [Data Collection](#data-collection)
- [System Integration](#system-integration)
- [Software Development Kit (SDK)](#software-development-kit-sdk)
- [Applications](#applications)
- [Future Development](#future-development)
- [Contributing](#contributing)
- [License](#license)
- [Summary](#summary)

## Project Goals

The primary goal is to build a functional prototype of the wearable health monitor, focusing on a complete hardware architecture that integrates sensors effectively. The design emphasizes cost-effectiveness for easy adaptation in commercial healthcare environments, ensuring it can fit various needs without high expenses.

Key objectives:
- Develop a generic, adaptable hardware setup that works across different healthcare scenarios.
- Prioritize sensor roles and data accuracy for reliable monitoring.
- After prototyping, design and fabricate a custom PCB with SMD modules for optimized production and scalability.

This approach aims to create a practical, affordable solution for the healthcare industry.

## Hardware Components and Sensor Roles

The hardware architecture is designed for cost-effectiveness and adaptability, using standard, affordable components that can be easily sourced and integrated. This ensures the prototype is functional and scalable for commercial healthcare use.

### Microcontroller
* **ESP32-C6 Module**: A small, energy-efficient processor with wireless features for handling sensor data and connectivity.

    <img width="auto" height="200" alt="image" src="assets/487221395-ad684b79-3f96-4360-80c6-31ebb8745015.png" />
    <img width="auto" height="200" alt="image" src="assets/XIAO-ESP32C6-4.png" />
    <img width="auto" height="200" alt="image" src="assets/F6EL5HNM3ZWC6J3.png" />

### Sensors
* **Pulse Oximeter and Heart Rate Sensor**
  - **Technology**: Measures blood oxygen levels and heart rate using light-based technology.
  - **Role**: Main tool for heart and circulation monitoring.
  - **Functions**: Captures signals to determine heart rate and oxygen levels, detects irregularities, and supports early alerts.

    <img width="auto" height="200" alt="image" src="assets/487228208-28cd40a6-15fe-4358-bb83-1c2087b71c4a.png" />
    <img width="auto" height="200" alt="image" src="assets/487228916-00e2713d-bbf1-4c84-8683-0cc38eb209a7.png" />

* **Body Temperature Sensor**
  - **Technology**: Tracks skin temperature for detecting fevers and monitoring thermal changes.
  - **Role**: Monitors temperature for infection detection and metabolic insights.
  - **Functions**: Measures skin temperature to identify fevers, track patterns, and provide context for other vital signs.

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
The device continuously gathers key health metrics in real-time: heart rate, blood oxygen levels, body temperature, heart rate variability, and activity data. These non-invasive measurements enable proactive health management.

## System Integration

To build an effective wearable system, components must work together smoothly for data flow and communication:

* **Sensor Connection**: Sensors link to the microcontroller using standard interfaces, enabling coordinated data gathering. The processor converts raw data into useful health metrics.
* **Wireless Features**: Includes Bluetooth and Wi-Fi for short-range and internet-based data transfer. Bluetooth connects to nearby devices like phones, while Wi-Fi allows direct cloud uploads.
* **Power Efficiency**: Optimized energy use keeps the device running longer on battery power, with smart modes for continuous monitoring.
* **Data Processing**: The microcontroller combines inputs from sensors into organized data packets for reliable transmission.
* **Network Expansion**: For multiple devices, wearables can connect in networks or through hubs that relay data to cloud services or healthcare platforms.

This setup creates reliable data pathways from the device to user applications.

## Software Development Kit (SDK)

The project includes an SDK for easy integration with other systems:

* **APIs**: Access real-time and historical health data.
* **Data Formats**: Supports standard formats like JSON and HL7 FHIR.
* **Security**: Secure authentication to protect data and comply with regulations.
* **Libraries**: Tools for common programming languages to embed data.
* **Customization**: Configure alerts and behaviors for specific needs.

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

## Future Development

Once the prototype is complete, the next steps include:
- Designing and fabricating a custom PCB with integrated SMD modules for improved efficiency and reduced costs.
- Expanding the SDK with more features for broader healthcare integrations.
- Testing in real-world clinical settings for validation and refinements.
- Exploring partnerships for commercial production and distribution.

Contributions and feedback are welcome to advance this project.

## Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details on how to get started.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Summary

A wearable health monitor IoT device with an SDK for healthcare integration. It tracks vital signs for early alerts and remote care, connecting to broader health systems for better outcomes in chronic care and recovery. The project focuses on building a cost-effective prototype with adaptable hardware, leading to custom PCB fabrication for scalable production.
