**ESPHome Xtend WiFi-Wifi Configuration**
Complete ESPHome configuration for monitoring an Intergas Xtend heat pump with two stacked ESP32 microcontrollers connected via UART (esp-1 & esp-2).

🎯 Overview
This project enables real-time monitoring of 66+ sensors from your Intergas Xtend heat pump system, integrating seamlessly with Home Assistant and uses ESPhome.io

**Hardware Setup**
ESP-1 (UART Bridge): Communicates with the heat pump via UART serial connection

ESP-2 (Master/WiFi): Handles WiFi connectivity and Home Assistant integration

Connection: Two ESP32 boards stacked and connected via UART pins (RX/TX) 

In my case I have soldered a female pin row and a male pin row and placed 2 ESP32 board on top of each other (stacked).

Only 1 board needs to be powered:
<img width="313" height="233" alt="image" src="https://github.com/user-attachments/assets/251ef023-6764-42bf-aeac-7c378c0783f6" />

<img width="318" height="366" alt="image" src="https://github.com/user-attachments/assets/8fb8eb4b-185a-4cfb-b071-2ee483100aed" />

Example of result:
<img width="1245" height="1788" alt="image" src="https://github.com/user-attachments/assets/6022e854-4cdf-4874-9f3e-cee2f3b2da07" />
