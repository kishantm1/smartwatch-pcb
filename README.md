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

<img src="images/Smartwatch%20Testing.png" alt="Testing setup" width="500" height="500">

## Final Board

**Front side**

<img src="images/Smartwatch%20Final%20Front.JPG" alt="Final board front side" width="500" height="500">

**Back side**

<img src="images/Smartwatch%20Final%20Back.png" alt="Final board back side" width="500">

## Firmware

The firmware runs on the ESP32-S3 and ties together everything the watch does from reading sensors, driving the display, handling touch input, and communicating wirelessly over both Bluetooth and WiFi. Rather than pausing to wait on one task before starting the next, each subsystem (sensor sampling, display redraws, BLE updates) runs on its own independent timer. Sensors are read once a second, the screen redraws once a second, and BLE pushes updates every five seconds, but none of these ever block each other. Touch input is checked continuously in between, so the watch always feels responsive instead of freezing while it waits on a sensor or a network request.

### Motion Sensing & Step Tracking

Motion is measured with a 6-axis IMU (accelerometer + gyroscope), connected to the ESP32-S3 over I2C. Rather than calculating steps in software from raw motion data, the firmware offloads step detection to the pedometer algorithm built directly into the IMU itself. The IMU's embedded pedometer engine detects step patterns on-chip and maintains an internal step counter that the ESP32-S3 reads during operation. This reduces processing overhead on the ESP32-S3 by allowing the IMU's dedicated hardware engine to handle step detection.

### Temperature & Environmental Sensing

Skin temperature and barometric pressure are read from two more I2C sensors. The pressure sensor's raw reading is converted into an estimated altitude using a standard atmospheric pressure formula, since pressure decreases predictably with elevation. Both values feed directly into the on-screen health and environment displays.

### Time & Location Awareness

The watch figures out where it is and what time it is without ever needing to pair with a phone. On boot, the watch connects to WiFi and queries a geolocation API using its public IP address. This returns both approximate coordinates and a UTC time zone offset, without requiring GPS hardware. Separately, the watch syncs its clock over the network using NTP (Network Time Protocol), which provides an accurate current time from public time servers, but only in UTC. Since NTP alone doesn't know what time zone the watch is actually in, the geolocation offset is applied on top of that synced time to shift it to the correct local time. The same location lookup also feeds current local weather conditions, so a single lookup on boot supports both features and avoids relying on any hardcoded location.

### Bluetooth Connectivity

The ESP32-S3 runs a Bluetooth Low Energy (BLE) GATT server that organizes the watch's sensor data, including step count, skin temperature, pressure, and altitude, as a set of services and characteristics that any nearby device can connect to. This was confirmed using a generic BLE inspection app, LightBlue, which connected to the watch and read back the correct decoded value for each characteristic. The image shows the app discovered the watch's custom Health Service along with its four characteristics.

<img src="images/Smartwatch%20BLE%20Connectivity.jpg" alt="BLE app showing connected SmartWatch GATT services" width="500" height="600">

### Touchscreen Navigation

Navigation is handled by a capacitive touch controller, also connected over I2C. Rather than continuously polling the controller to check for input, the firmware relies on an interrupt. The touch controller itself signals the ESP32 the instant a gesture occurs. Swipe gestures move between the watch's three screens.

### On-Device Display

The firmware maintains a central watch state containing the latest sensor measurements, connectivity status, and interface state. Each screen reads from this shared state and renders the corresponding information to the display.

**Home screen: Time, Date, Bluetooth & Battery Status**

<img src="images/Smartwatch%20Home%20Screen.png" alt="Smartwatch home screen showing time, date, Bluetooth status, and battery status" width="500" height="500">

**Health screen: Step Count & Skin Temperature**

<img src="images/Smartwatch%20Health%20Screen%20.png" alt="Smartwatch health screen showing step count and skin temperature" width="500" height="500">

**Environment screen: Weather, Barometric Pressure & Altitude**

<img src="images/Smartwatch%20Environment%20Screen.png" alt="Smartwatch Environment Screen" width="500" height="500">

