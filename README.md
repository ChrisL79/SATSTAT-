# SATSTAT QO-100 Station Monitor

SATSTAT is an open source station monitor for QO-100 (Es'hail-2) satellite operators. It connects to a DXPatrol QO-100 amplifier via an ESP32 microcontroller and provides real time monitoring of your station over WiFi through any web browser or the dedicated Windows desktop application.

---

## Features

- Live forward and reflected power metering
- Peak power hold
- SWR monitoring
- Dual DS18B20 temperature monitoring (amplifier and transverter)
- Dual INA219 voltage and current monitoring
- PTT inhibit relay control
- WiFi signal strength and ESP32 temperature monitoring
- Dark mode
- OTA (Over The Air) firmware updates
- Captive portal WiFi setup — no code editing required
- Windows desktop application with auto network discovery
- Fully calibratable via browser interface

---

## Hardware Required

- ESP32-C5
- DXPatrol QO-100 amplifier
- 2x INA219 I2C current/voltage sensor modules
- 2x DS18B20 temperature sensors
- 1x relay module for PTT inhibit
- Resistors for voltage divider (1k, 2k, 1k)

---

## Author

Chris Lawton M7JEX — Made with love in Somerset, United Kingdom.
