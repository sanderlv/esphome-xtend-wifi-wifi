**ESPHome Xtend WiFi-Wifi Configuration**

Complete ESPHome configuration for monitoring an Intergas Xtend heat pump with two stacked ESP32 microcontrollers connected via UART (esp-1 & esp-2).

**🎯 Overview**

This project enables real-time monitoring of 66+ sensors from your Intergas Xtend heat pump system, integrating seamlessly with Home Assistant and uses ESPhome.io

**Hardware Setup**

ESP-1 (Xtend side): Connects to the Xtend's own WiFi access point, polls its local API every 10 s and forwards the JSON to ESP-2 over UART

ESP-2 (Home side): Connects to your home WiFi, parses the data and publishes it to Home Assistant via the ESPHome API

Connection: Two ESP32 boards stacked and connected via UART pins (RX/TX) 

In my case I have soldered a female pin row and a male pin row and placed 2 ESP32 board on top of each other (stacked).

Only 1 board needs to be powered:

<img width="313" height="233" alt="image" src="https://github.com/user-attachments/assets/251ef023-6764-42bf-aeac-7c378c0783f6" />

<img width="318" height="366" alt="image" src="https://github.com/user-attachments/assets/8fb8eb4b-185a-4cfb-b071-2ee483100aed" />

**Wiring**

| ESP-1 | ESP-2 | Purpose |
|---|---|---|
| GPIO16 (TX) | GPIO16 (RX) | Xtend data, ESP-1 to ESP-2 |
| GPIO18 (RX) | GPIO18 (TX) | Commands, ESP-2 to ESP-1 (maintenance / restart) |
| GND | GND | |
| 5V | 5V | Power one board, the other is fed through this pin |

**Configuration**

- `esp-1.yaml`: set `xtend_ssid` / `xtend_password` (your Xtend's WiFi) and `home_ssid` / `home_password` (your home WiFi, only used for OTA).
- `esp-2.yaml`: set `ssid` / `password` for your home WiFi and add `Fallback_Hotspot` to your `secrets.yaml`.
- ESP-1 deliberately has no `api:`. It can never reach Home Assistant, and with `api:` but no client ESPHome reboots it every 15 minutes.

**OTA updates for ESP-1**

ESP-1 lives on the Xtend's network, so it is not reachable for normal OTA. Press **Xtend Poller Maintenance Mode** on ESP-2 in Home Assistant: ESP-1 joins your home WiFi for 10 minutes and can then be flashed wirelessly from the ESPHome dashboard. Any reboot, including the one after the update, sends it back to the Xtend WiFi. Give ESP-1 a DHCP reservation and set it as `use_address` so the dashboard can find it. The very first flash of ESP-1 has to be done over USB.

**Diagnostics**

- **Xtend Data OK**: off when no Xtend data arrived for 60 s; the numeric sensors then go to unknown instead of freezing at their last value.
- Fields the Xtend reports as not available (32767) show as unknown. Not every Xtend/boiler combination provides **Xtend Boiler, CH Water, Return**, and **Xtend Boiler, CH Water, Setpoint** only has a value while the Xtend asks the boiler (CV ketel) for heat.
- **Xtend API Reachable**, **Xtend Poller Link**, **Xtend Poller WiFi Signal / Uptime / SSID / IP**: health of ESP-1 and its link to the Xtend.
- **Xtend Poller Restart**: remote restart of ESP-1.

Example of result:
<img width="423" height="1358" alt="image" src="https://github.com/user-attachments/assets/8da9e28a-c9f6-44da-8721-6e3009c3753a" />

Met hulp van: 
https://github.com/thomasvt1/xtend-bridge/blob/main/parse-message.js
https://github.com/WillemD61/XTEND-plugin
https://github.com/thomasvt1/xtend-bridge
https://github.com/DSchoutsen/HA_connection_Xtend
