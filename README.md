# Wearable Smartwatch PCB 

Wearable smartwatch PCB based on ESP32-S3 integrating IMU-based step tracking, temperature sensing, barometric pressure sensing, Bluetooth connectivity, and display/touch interfaces. This project focused on end-to-end wearable hardware development, including BOM creation, schematic design, PCB layout, reflow soldering, board testing, and firmware development.

## Key Features

- Wrist-worn smartwatch form factor
- Touch/display interface for on-device navigation
- Main screen with time, battery status, and Bluetooth status
- Health screen with skin temperature and step tracking
- Environment screen with barometric pressure and weather
- 3.7V battery-powered design

## Hardware Architecture

The board is centered around the ESP32-S3 microcontroller and integrates sensing, display, power, and programming/debug circuitry into a compact smartwatch PCB.

- **MCU:** ESP32-S3
- **Motion sensing:** IMU for motion and step tracking
- **Environmental sensing:** Temperature sensor and barometric pressure sensor
- **Sensor communication:** I2C sensor interfaces
- **Wireless communication:** Bluetooth/BLE through the ESP32-S3
- **Display/UI:** Touchscreen display for time, health data, and environmental data
- **Display communication:** SPI display interface
- **Power:** 3.7V LiPo battery
- **Debug/programming:** Boot and reset support circuitry

## Schematic

### MCU

### Sensors

### Power

### Display

## Layout
The 2-layer PCB layout was designed to fit within a compact smartwatch form factor while routing sensor, display/touch, and power connections.

## 3D View

## Assembly 
The board was assembled using solder paste, manual component placement, and reflow soldering.

## Testing 
Initial testing focused on basic board functionality and power validation.

Testing included:
- Checking for shorts
- Verifying power delivery
- Checking sensor behavior
- Testing I2C connection to connected ICs

## Final Board




