**************************************************************
*** SATSTAT QO-100 Station Monitor User Instructions ***
**************************************************************

**************************************************************
*** WHAT IS SATSTAT? ***
**************************************************************

SATSTAT is a complete web-based station monitor for your QO-100 (Es’hail-2) satellite setup.

It displays in real time:

Forward power (FWD) and peak power (with 1-second peak-hold).
Reflected power (with 1-second peak-hold and red warning if >1.8).
XVTR temperature, voltage and current.
Amplifier temperature, voltage and current.
ESP32 internal temperature and WiFi signal strength.
IP address and SSID.
PTT Inhibit relay control (via SAFE / ARMED switch).

Everything is viewed from any phone, tablet or computer on your WiFi network, or remotely if you set up a VPN.

***************************************************************
*** WHAT YOU NEED ***
***************************************************************

1) 1 ESP32C5 development board (DevKit or similar). Must be the C5 version or equivalent to use 5ghz, 2ghz will not work in this project for obvious reasons.

2) 2 INA219 current/voltage sensors (i used addresses 0x41 for XVTR, 0x44 for AMP so modules could be on same bus).

3) 2 DS18B20 temperature sensors (one for XVTR and one for AMP).

4) 1 12v Relay module on pin 9 for PTT inhibit. I used 2 modules, one for PTT inhibit and one to isolate the amp from the transverter as the transverter would lock up during TX.

5) You must make a 1k-2k-1k voltage divider as the maximum voltage allowed on the GPIO pins is 3.3v. At higher RF outputs, the DXPatrol amp will have well over 3.3v on the sense wires which will damage your ESP unit.

6) Buck converter to supply the ESP32C5 with power. I took the feed from the 24v amp supply.

7) Waterproof enclosure.

8) Various consumables such as male/female mic connectors, cable, cable entry glands etc...

9) Beer!

***************************************************************
***PREREQUISITES***
***************************************************************

Step 1: Download and install the following libraries:

WiFi.h
WebServer.h
math.h
Wire.h
Adafruit_INA219.h
OneWireNg_CurrentPlatform.h
drivers/DSTherm.h
utils/Placeholder.h
FS.h
SPIFFS.h
ArduinoOTA.h

Step 2: Install ESP32C5 from board manager.

Step 3: First upload (USB)

Open the Arduino IDE.
Paste the full code.
Select your ESP32 board and the correct COM port.
Click Upload.
Open the Serial Monitor (115200 baud) and wait until you see it connect to your WiFi.

Step 2: Connect to WiFi
The ESP32 will automatically connect to the WiFi network you set in the code.

Step 3: First-time setup (one-time only)
When you first open the monitor in a browser you will see a setup screen:

Enter your CALLSIGN and LOCATOR.
Choose Use Default Table (recommended) or enter your own data in the Custom Table fields.

Click SAVE & SHOW MONITOR.

The page will reload and you will see the main dashboard.
Your callsign and locator are saved permanently in the browser.

***************************************************************
***HOW TO USE THE GUI***
***************************************************************

Step 4: How to use the dashboard

Open any browser and go to the ESP32’s IP address (shown in the ESP32 STATUS box at the bottom).
The screen shows:

Big FWD and REF bars (green/red) with peak-hold markers (red lines).
XVTR and AMP data grids showing voltage, current and temperature.
ESP32 temperature and WiFi signal bars.
PTT INHIBIT switch (toggle it to enable/disable the relay).

Dark mode – tap the moon icon in the bottom-right box.
Settings – tap the gear icon to change callsign, locator or calibration.
Info – tap the “i” icon for version and author info.

Step 5: Updating the firmware over WiFi (OTA)
You no longer need a USB cable for updates!

Make any changes to the code in the Arduino IDE.
Go to Tools → Port.
You will now see an entry called SATSTAT (it may take 10–20 seconds to appear).
Select SATSTAT.
Click Upload.

The ESP32 will receive the new firmware wirelessly.
It keeps your WiFi settings and calibration data.
OTA password = SATSTATOTA.

*****************************************************************
***Quick Tips***
*****************************************************************

The first upload must be done with USB.
After that, all future updates can be done over WiFi.
If you ever want to factory-reset calibration, just choose “Use Default Table” again in the setup screen.
The PTT INHIBIT relay starts in the OFF (SAFE) state every time the ESP32 boots.

You’re all set!

Just open your browser, go to the IP address shown on the ESP32 STATUS box, and you have a real-time QO-100 station monitor.

Here are the GIPO pins i have used. You can change these in the code to whatever works for your particular wiring environment.

******************************************************************
***GPIO PINOUTS***
******************************************************************
GND - System tie bus for 5v, 13.8v and 24v.
5V - 5v input from the buck converter. Powers the ESP32C5.
GPIO4 - RF
GPIO5 - REF
GPIO23 - SDA FROM INA219
GPIO24 - SCL FROM INA219
GPIO25 - TEMP INPUT FROM AMP SENSOR
GPIO26 - TEMP INPUT FROM XVTR SENSOR
GPIO9 - PTT INHIBIT RELAY

******************************************************************
***DISCLAIMER***
******************************************************************

I TAKE NO RESPONSIBILITY FOR ANY DAMAGE CAUSED TO YOUR EQUIPMENT. THIS IS QUITE A SIMPLE AND FUN PROJECT TO MAKE, BUT YOU HAVE TO TAKE RESPONSIBILITY FOR YOUR OWN ACTIONS. YOU ARE THE ONE OPERATING THE CONTROLS IN YOUR HEAD...NOT ME.
THIS SOFTWARE IS PROVIDED FREE TO THE COMMUNITY AND OFFERED IN GOOD SPIRIT. IF YOU ARE NOT CONFIDENT IN YOUR OWN ABILITIES TO BUILD AND WIRE THIS PROJECT INTO YOUR STATION, THEN PLEASE DO NOT PROCEED...OR GET SOMEONE COMPETENT TO HELP YOU...YOU MAY EVEN LEARN A NEW SKILL!

HAPPY BUILDING...M7JEX (CHRIS).
