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
- **Power:** 3.7V LiPo battery with USB-C charging and regulated 3.3V system power
- **Debug/programming:** Boot and reset support circuitry
- **Indicators:** Status LED for board/charging indication

## Schematic

### MCU

![MCU Schematic](images/Smartwatch%20MCU%20Schematic.png)

### Sensors

![Sensors Schematic](images/Smartwatch%20Sensors%20Schematic.png)

### Power

![Power Schematic](images/Smartwatch%20Power%20Schematic.png)

### Display

![Display Schematic](images/Smartwatch%20Display%20Schematic.png)

## Layout

The 2-layer PCB layout was designed to fit within a compact smartwatch form factor while routing sensor, display/touch, and power connections.

<img src="images/Smartwatch%20Layout.png" alt="PCB Layout" width="700">

## 3D View

<img src="images/Smartwatch%203D%20Viewer.png" alt="3D View" width="600">
## Assembly 

The board was assembled using solder paste, manual component placement, and reflow soldering.

**Solder paste applied**

![Solder Paste](images/Smartwatch%20Solder%20Paste.png)

**Components placed**

![Reflow Components](images/Smartwatch%20Reflow%20Components.png)

**After heating in oven**

![Reflow Finished](images/Smartwatch%20Reflow%20Finished.png)

## Testing 

Initial testing focused on basic board functionality and power validation.

Testing included:
- Checking for shorts
- Verifying power delivery
- Checking sensor behavior
- Testing I2C connection to connected ICs

<img src="images/Smartwatch%20Testing.png" alt="Testing setup" width="450">

## Final Board

**Front side**

<img src="images/Smartwatch%20Final%20Front.JPG" alt="Final board front side" width="500">

**Back side**

<img src="images/Smartwatch%20Final%20Back.png" alt="Final board back side" width="500">

## Firmware

Firmware development is currently underway. The current firmware supports on-device display screens for health and environmental data, including step count, skin temperature, and weather, barometric pressure, and altitude.

**Health screen: Step Count & Skin Temperature**

<img src="images/Smartwatch%20Final.png" alt="Watch display on wrist" width="500">

**Environment screen: Weather, Barometric Pressure & Altitude**

<img src="images/Smartwatch%20Environment%20Screen%20.png" alt="Smartwatch Environment Screen" width="500">

