# SATSTAT QO-100 Station Monitor
### By Chris Lawton M7JEX

SatStat is an open source station monitor for QO-100 (Es'hail-2) satellite operators. It connects to a DXPatrol QO-100 amplifier via an ESP32-C5 microcontroller, (or any other amp with a voltage sense wire for FWD and REF power) and provides real time monitoring of your station over WiFi through any web browser or the dedicated Windows desktop application.

---

![SATSTAT Windows App in Action](VIDEO.gif)

---

![SATSTAT Browser Interface](IMAGES/1.jpg)
![SATSTAT Windows App](IMAGES/2.jpg)

---

## Features

- Live forward and reflected power metering with peak hold
- SWR monitoring
- Dual DS18B20 temperature monitoring (amplifier and transverter)
- Dual INA219 voltage and current monitoring (amplifier and transverter)
- PTT inhibit relay control
- WiFi signal strength and ESP32 temperature monitoring
- Dark mode
- OTA firmware updates. No USB cable needed after first flash
- Captive portal WiFi setup. No code editing required
- Windows desktop application with automatic network discovery
- Fully calibratable via browser interface or Windows program

---

## The Station

![SATSTAT in its enclosure](IMAGES/3.jpg)
![SATSTAT enclosure](IMAGES/4.jpg)
![SATSTAT enclosure](IMAGES/5.jpg)
![SATSTAT enclosure](IMAGES/6.jpg)
![SATSTAT enclosure](IMAGES/7.jpg)

![Transverter](IMAGES/8.jpg)
![Transverter](IMAGES/9.jpg)
![Transverter](IMAGES/10.jpg)
![Transverter](IMAGES/11.jpg)
![Transverter](IMAGES/12.jpg)

![QO-100 Dish and Station Setup](IMAGES/13.jpg)
![QO-100 Dish and Station Setup](IMAGES/14.jpg)
![QO-100 Dish and Station Setup](IMAGES/15.jpg)
![QO-100 Dish and Station Setup](IMAGES/16.jpg)
![QO-100 Dish and Station Setup](IMAGES/17.jpg)
![QO-100 Dish and Station Setup](IMAGES/18.jpg)

![Amplifier Calibration](IMAGES/19.jpg)

---

## Hardware Required

- ESP32-C5 development board (a 2.4 ghz board will NOT work for obvious reasons)!
- DXPatrol QO-100 amplifier (or similar with sense output)
- 2x INA219 I2C current/voltage sensor modules (addresses 0x41 and 0x44)
- 2x DS18B20 temperature sensors (OneWire)
- 1x 12v relay module for PTT inhibit
- 1x Buck converter to power the ESP32C5
- Resistors: 1kΩ, 2kΩ, 1kΩ (voltage divider for sense lines)
- Enclosure of your choice
- DC power supply from either your amp or transverter via buck converter to power the ESP32C5

---

## Schematic

![SATSTAT Schematic](SatStat%20Schematic.jpg)

Full schematic: [SatStat Schematic](SatStat%20Schematic.jpg)

---

## ESP32-C5 Pin Assignments

![ESP32-C5 Pinout](ESP32C5%20PINOUT.jpg)

| GPIO | Function |
|------|----------|
| GPIO 4 | FWD power sense ADC (via voltage divider) |
| GPIO 5 | REF power sense ADC (via voltage divider) |
| GPIO 9 | PTT inhibit relay output |
| GPIO 23 | I2C SDA (INA219 sensors) |
| GPIO 24 | I2C SCL (INA219 sensors) |
| GPIO 25 | AMP DS18B20 temperature sensor |
| GPIO 26 | XVTR DS18B20 temperature sensor |

---

## Software Setup

### ESP32 Firmware

1. Install [Arduino IDE](https://www.arduino.cc/en/software)
2. Add ESP32 board support in Arduino IDE
3. Install the following libraries:
   - Adafruit INA219
   - OneWireNg
   - WiFiManager
4. Open `satstat.ino` in Arduino IDE
5. Select your ESP32-C5 board
6. Flash to your ESP32-C5 via USB

### First Time WiFi Setup

1. On first boot the ESP32 creates a WiFi access point named **SATSTAT-Setup**
2. Connect to **SATSTAT-Setup** from your phone browser or PC
3. A captive portal will appear — enter your home WiFi credentials
4. The ESP32 will connect to your network and restart
5. Open a browser and navigate to the ESP32 IP address
6. Complete the station setup screen (callsign, locator, calibration tables if needed)

### OTA Updates

Once connected to WiFi, future firmware updates can be done wirelessly:
- **Hostname:** SATSTAT
- **Password:** SATSTATOTA
- SATSTAT will appear under Network Ports in Arduino IDE

To reset WiFi credentials navigate to: `http://[ESP32-IP]/resetwifi`

---

## Windows Application

The SATSTAT Windows application automatically discovers your ESP32 on the local network and displays all station data in a native desktop window.

### Installation

1. Download `SATSTAT Setup 1.0.0.exe` from the releases section
2. Run the installer and follow the on screen instructions
3. Launch SATSTAT from your desktop or Start Menu
4. The app will automatically find your ESP32 on the network

---

## Calibration

### Forward Power Table

The default FWD lookup table is calibrated for the DXPatrol QO-100 amplifier. If you have a different amplifier, measure your own sense voltage at known power levels and enter a custom table in the setup screen.

### REF / SWR Table

For the new version DXPatrol amp the REF sense output is:
- **1.5V at 1:1 SWR** (perfect match)
- **4.0V at infinite SWR**

Enter your own measured values for accurate reflected power readings.

### ADC Calibration Factors

Three calibration factors correct for ESP32 ADC non-linearity across the voltage range. Adjust these in the setup screen if your power readings are inaccurate.

---

## Notes

- Default lookup tables are calibrated for the DXPatrol QO-100 amplifier
- If your REF bar reads high into a dummy load your amp's directional coupler may have poor isolation — this is a known issue with some units (mine included)!
- The quality of DXPatrol amps is not consistent between units — measure and calibrate your own
- Thanks to Mike M0ABR for the watts/volts dataset and use of the power meter

---

## License

Free for amateur radio community use and modification.
Commercial sale or redistribution for profit is strictly prohibited.
Use at your own risk.

---

## Author

**Chris Lawton M7JEX**
Made with love in Somerset, United Kingdom.

[QRZBook](https://www.qrzbook.net) — A community for radio enthusiasts from around the globe.
[Kloudlogger](https://www.kloudlogger.com) — An online cloud based full featured logging program.
