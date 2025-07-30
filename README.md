# Arduino BLE FlexiForce Sensor Project

**Group:** The Alligators  
**Course:** BMEN 3030 - Bioinstrumentation

## Overview

This project implements a Bluetooth Low Energy (BLE) sensor system using an Arduino MKR WiFi 1010 to read data from three FlexiForce pressure sensors and transmit the readings wirelessly to paired devices.

## Hardware Requirements

- Arduino MKR WiFi 1010
- 3x FlexiForce Pressure Sensors
- Connecting wires
- Breadboard (optional)
- 3x 10kΩ resistors (for voltage divider circuits)

## Pin Configuration

| Component | Arduino Pin |
|-----------|-------------|
| FlexiForce Sensor 1 | A1 |
| FlexiForce Sensor 2 | A2 |
| FlexiForce Sensor 3 | A3 |

## Wiring Diagram

Each FlexiForce sensor should be connected in a voltage divider configuration:

```
3.3V ── FlexiForce Sensor ── Analog Pin (A1/A2/A3)
                          │
                          └── 10kΩ Resistor ── GND
```

## Software Dependencies

- **ArduinoBLE Library**: Install through Arduino IDE Library Manager
  - Go to Sketch → Include Library → Manage Libraries
  - Search for "ArduinoBLE" and install the latest version

## BLE Service Configuration

- **Service UUID:** `19b10010-e8f2-537e-4f6c-d104768a1214`
- **Sensor 1 Characteristic:** `19b10011-e8f2-537e-4f6c-d104768a1214`
- **Sensor 2 Characteristic:** `19b10012-e8f2-537e-4f6c-d104768a1214`
- **Sensor 3 Characteristic:** `19b10013-e8f2-537e-4f6c-d104768a1214`

All characteristics support both READ and NOTIFY operations.

## Features

- **Wireless Data Transmission**: Sends sensor readings via Bluetooth Low Energy
- **Real-time Monitoring**: Serial monitor displays sensor values every 700ms
- **Calibrated Readings**: Applies calibration factor (80x) to raw sensor values
- **Multi-sensor Support**: Handles three pressure sensors simultaneously
- **Connection Status**: Displays BLE connection status and client address

## Installation & Setup

1. **Hardware Setup:**
   - Connect the three FlexiForce sensors to analog pins A1, A2, and A3
   - Ensure proper voltage divider configuration with 10kΩ resistors

2. **Software Setup:**
   - Install the ArduinoBLE library
   - Upload the code to your Arduino MKR WiFi 1010
   - Open Serial Monitor at 9600 baud rate

3. **BLE Connection:**
   - The device advertises as "MKR Wifi 1010"
   - Use a BLE scanner app or custom application to connect
   - Subscribe to characteristics to receive sensor notifications

## Usage

1. Power on the Arduino MKR WiFi 1010
2. Wait for "Bluetooth device active, waiting for connections..." message
3. Connect to the device using a BLE-enabled device or application
4. Monitor sensor readings in the Serial Monitor or through BLE notifications
5. Apply pressure to the FlexiForce sensors to see value changes

## Data Format

- **Raw Reading Range:** 0-1023 (10-bit ADC)
- **Voltage Conversion:** `(reading × 3.3V) / 1023`
- **Calibrated Output:** `voltage × calibration_factor (80)`
- **Update Rate:** Every 700ms

## Troubleshooting

**BLE Connection Issues:**
- Ensure the ArduinoBLE library is properly installed
- Check that no other devices are connected to the Arduino
- Verify the Arduino MKR WiFi 1010 is powered correctly

**Sensor Reading Problems:**
- Verify wiring connections to analog pins
- Check that FlexiForce sensors are properly connected in voltage divider configuration
- Ensure 10kΩ pull-down resistors are connected

**Serial Monitor Issues:**
- Set baud rate to 9600
- Check USB connection
- Press the reset button on the Arduino if needed

## Calibration

The current calibration factor is set to 80. To adjust:
1. Modify the `cf` constant in the code
2. Re-upload the sketch
3. Test with known force values to verify accuracy

## Applications

This system can be used for:
- Pressure monitoring in biomedical devices
- Force measurement in rehabilitation equipment
- Load sensing in prosthetic devices
- Research applications requiring wireless pressure data

## Technical Specifications

- **Operating Voltage:** 3.3V
- **ADC Resolution:** 10-bit (0-1023)
- **BLE Protocol:** Bluetooth Low Energy 4.0+
- **Data Type:** 32-bit Float
- **Transmission Range:** ~10 meters (typical BLE range)

## License

This project is developed for educational purposes as part of BMEN 3030 - Bioinstrumentation coursework.

## Support

For technical support or questions about this project, please contact the development team or refer to the Arduino MKR WiFi 1010 and ArduinoBLE documentation.