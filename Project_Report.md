# IoT-Based Smart Energy Monitoring System

## Abstract
This project monitors the electrical parameters of a low-voltage DC load using an INA219 sensor and ESP32. The ESP32 reads voltage and current, calculates power and accumulated energy, and uploads the readings to ThingSpeak through Wi-Fi for remote monitoring.

## Objectives
- Measure voltage and current.
- Calculate power.
- Estimate accumulated energy.
- Upload readings to an IoT cloud platform.
- Enable remote monitoring.

## Working
The INA219 measures voltage and current. ESP32 receives the values through I2C. Power is calculated as P = V × I. Energy is accumulated using power and elapsed time. ESP32 connects to Wi-Fi and sends the values to ThingSpeak.

## Block Diagram
Low-voltage DC Load → INA219 → ESP32 → Wi-Fi → ThingSpeak Cloud → Dashboard

## Expected Result
Voltage, current, power and accumulated energy are displayed in the Serial Monitor and uploaded to the ThingSpeak dashboard.

## Future Scope
OLED display, electricity-cost calculation, alerts, historical reports and a mobile dashboard can be added.

## Safety
Use only a low-voltage DC demonstration setup. Do not connect ESP32/INA219 directly to 230 V AC mains.
