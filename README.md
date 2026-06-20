ESPHome Xtend WiFi Configuration
Complete ESPHome configuration for monitoring an Intergas Xtend heat pump with two stacked ESP32 microcontrollers connected via UART.

🎯 Overview
This project enables real-time monitoring of 66+ sensors from your Intergas Xtend heat pump system, integrating seamlessly with Home Assistant.

Hardware Setup
ESP-1 (Master/WiFi): Handles WiFi connectivity and Home Assistant integration
ESP-2 (UART Bridge): Communicates with the heat pump via UART serial connection
Connection: Two ESP32 boards stacked and connected via UART pins (RX/TX)
