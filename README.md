# IoT-Based Smart Energy Monitoring System

An ESP32 + INA219 project that measures voltage, current, power and accumulated energy, then uploads the readings to ThingSpeak through Wi-Fi.

## Hardware
- ESP32
- INA219 sensor
- Low-voltage DC supply
- Suitable low-voltage DC load
- Jumper wires
- USB cable

## Software
- Arduino IDE
- ESP32 board support
- Adafruit INA219 library
- ThingSpeak library

## I2C wiring
- INA219 VCC -> ESP32 3.3V
- INA219 GND -> ESP32 GND
- INA219 SDA -> GPIO 21
- INA219 SCL -> GPIO 22

Place the INA219 appropriately in the low-voltage DC load circuit according to the sensor module instructions.

## ThingSpeak fields
Field 1 = Voltage (V)
Field 2 = Current (A)
Field 3 = Power (W)
Field 4 = Energy (Wh)

## Setup
1. Install Arduino IDE and ESP32 support.
2. Install Adafruit INA219 and ThingSpeak libraries.
3. Create a ThingSpeak channel with four fields.
4. Put your Wi-Fi name/password, Channel ID and Write API Key in the `.ino` file.
5. Select your ESP32 board and COM port.
6. Upload the program.
7. Open Serial Monitor at 115200 baud.
8. View the readings on ThingSpeak.

## Formula
Power (W) = Voltage (V) × Current (A)

## Safety
This project is designed for low-voltage DC demonstration. Never connect the ESP32, INA219 or breadboard directly to household 230 V AC mains.
