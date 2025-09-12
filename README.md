# Wearable Health Monitor (Prototype + SDK)

Simple wearable device concept for collecting basic vital data and sending it to other systems. Includes an SDK so software teams can ingest readings, store them, trigger alerts, or build dashboards. First phase: working prototype. Later phase: custom PCB.

## Project Scope

Near term:
- Build a bench prototype with off‑the‑shelf parts.
- Validate sensor signal quality and power profile.
- Define simple data model (timestamp + metric + quality flag).

After validation:
- Design custom PCB (SMD integration, reduced footprint).
- Reduce BOM cost and size.
- Prepare for enclosure + basic regulatory path.

Design principles: keep it small, low cost, reusable in different mounting formats, and easy to integrate.

## Hardware

### Microcontroller
* **ESP32-C6 module**: Wireless + compute; collects sensor data and sends packets.

    <img width="auto" height="200" alt="image" src="assets/487220664-93b4fa06-bbe1-46a4-bbbc-61eb7910c3b3.png" />
    <img width="auto" height="200" alt="image" src="assets/487221395-ad684b79-3f96-4360-80c6-31ebb8745015.png" />
* **Pulse oximeter / heart rate sensor**: SpO2 + pulse from PPG.

    <img width="auto" height="200" alt="image" src="assets/487228208-28cd40a6-15fe-4358-bb83-1c2087b71c4a.png" />
    <img width="auto" height="200" alt="image" src="assets/487228916-00e2713d-bbf1-4c84-8683-0cc38eb209a7.png" />

* **Skin temperature sensor**: Surface temperature trend.

    <img width="auto" height="200" alt="image" src="assets/487226981-cddb6d25-80e5-4128-9f71-87d094b1067b.png" />
    <img width="auto" height="200" alt="image" src="assets/487227354-0505348d-5cc2-422d-a15f-0a94faac48a8.png" />

### Approximate Module Sizes
* ESP32-C6: ~18 × 25.5 × 2.8 mm
* PPG sensor: ~5.6 × 3.3 × 1.6 mm
* Temp sensor: ~3 × 3 × 0.9 mm

## Physical Concept

Initial form: simple band or patch mount on arm / upper body. Flexible strap or adhesive cradle. Focus on sensor contact, stable pressure, and easy removal.

Core elements:
- Enclosure: small shell holding MCU, battery, sensors.
- Contact window: opening or lens for PPG emitter / detector.
- Haptic + LED (optional) for local status.
- Charging: wired (USB-C) or pogo pads in early phase; future: magnetic dock.
- Optional display (deferred).

## Data Points (Prototype Phase)
Minimum set:
* Heart rate (bpm)
* SpO2 (%)
* Skin temp (°C)
* Raw PPG (optional stream)
* Motion flag / movement level (optional later)

Each sample: timestamp, value(s), quality / confidence flag.

### Sample Data Packet (JSON)
```json
{
    "ts": "2025-09-12T10:15:23.412Z",
    "hr_bpm": 72,
    "spo2_pct": 97.4,
    "skin_temp_c": 34.1,
    "quality": "ok",
    "raw_ppg_ref": "ppg/2025/09/12/10/15/23_412.bin"
}
```
Notes:
* `raw_ppg_ref` optional; may point to a chunk file if streaming disabled.
* `quality` simple states: ok | motion | low_signal | error.

## Component Roles
* PPG sensor: light signal → pulse, SpO2, variability estimates.
* Temp sensor: skin temp trend, helps contextualize other readings.
* MCU (ESP32-C6): scheduling, preprocessing, wireless, power states.
* Battery + power circuit: supply + charging.
* Optional haptics / LED: minimal user feedback.

## System Architecture (Draft)
Layers:
1. Sensing (PPG, temp)
2. Sampling + preprocessing (filtering, averaging)
3. Packet builder (JSON / binary frame)
4. Transport (BLE GATT; Wi‑Fi / MQTT optional later)
5. Edge gateway / app (receives, validates, forwards)
6. Storage / analytics (out of scope here)

Power strategy: duty cycle sensors, burst transmit, low-power idle.

## SDK (Planned)
Deliverables:
* Data model (JSON schema + minimal FHIR mapping note)
* Reference ingestion API (REST)
* Simple BLE client example
* Language helpers (Python + JavaScript first)
* Alert hook interface (webhook stub)

Focus: keep surface small; enable quick prototype integrations.

## Prototype Roadmap (Draft)
Phase 0: Bench bring-up (dev boards, log raw signals)
Phase 1: Basic firmware loop (sampling + BLE broadcast)
Phase 2: Add temp + packet format + gateway script
Phase 3: Power tuning (duty cycle, sleep modes)
Phase 4: Rev A custom PCB (core + headers)
Phase 5: Rev B shrink + improved enclosure trial
Phase 6: Small pilot batch (<=25 units)

## Risks & Open Questions
* Motion artifacts: need filtering strategy + quality flag thresholds.
* Skin temp lag vs core temp: documentation clarity required.
* Battery life target (goal? 48h continuous?) not yet fixed.
* BLE vs Wi-Fi coexistence power cost not characterized.
* Enclosure sealing vs sensor window condensation.
* Regulatory path (medical vs wellness) still undecided.
* Data privacy model if cloud ingestion added later.

## Immediate Next Steps
1. Select exact PPG breakout + temp breakout.
2. Write minimal firmware: init sensors, sample HR/SpO2, print over serial.
3. Decide packet frequency (e.g. 1 Hz summary, optional raw buffer every 30 s).
4. Draft JSON schema file.
5. Simple Python receiver (BLE or serial) to log JSON lines.
6. Measure idle + active current (multimeter or INA219).
7. Record 10 min motion vs still dataset for quality logic.

## Nice To Have (Later)
* MQTT bridge example.
* Web dashboard stub.
* Basic over-the-air update flow.
* HRV derivation from PPG intervals.
* Simple alert rule engine (threshold + duration).

## Example Use Cases
* Remote monitoring (home recovery)
* Chronic condition tracking
* Elder support (basic vitals + trend flags)
* Research data collection
* Integration testbed for health platforms

## Deployment Contexts
* Home recovery
* Clinic trial kits
* Assisted living
* Developer lab / sandbox
* Future: multi-device gateway setups

## Summary
Prototype path: prove sensing + data pipeline, then shrink into custom PCB and light SDK so others can plug it in fast.

Scope is intentionally narrow: a small, low-cost, reusable vital capture node.
