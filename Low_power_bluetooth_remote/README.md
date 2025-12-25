# Bluetooth Remote Controller (ESP32)

## Overview
This project is a **low-power Bluetooth remote controller** using an ESP32-S3 MCU.  
It supports multiple buttons for controlling music playback and other Bluetooth HID commands. The design focuses on **low sleep current, clean grounding, proper power design, and reliable input handling**.  

The goal is not just a working remote, but a **portfolio-quality PCB demonstrating best practices in embedded hardware design**.

---

## Features

- ESP32-S3-WROOM-1 MCU (supports Bluetooth Low Energy)
- Up to 4 buttons (Bin1–Bin4)
- USB-C for power and programming
- Low dropout regulator for 3.3 V power supply
- Decoupling capacitors near power pins
- RC filters for buttons to suppress EMI
- Designed for low sleep current (<10 µA target)
- Clean ground plane with controlled high-current loops
- Optional LED indicators for button press feedback
- 2-layer PCB, designed for manufacturability

---

## Design Decisions

### 1. Power Design
- **Input:** USB 5 V  
- **Voltage Regulation:** AP63201 buck converter provides 3.3 V for MCU and peripherals.  
- **Decoupling:** 0.1–1 µF capacitors placed directly at power pins to reduce switching noise.  
- **Battery Support:** Li-ion support via MCP73831 charge IC (optional for standalone use).  
- **Sleep Current Optimization:** 
  - All unused GPIOs set to avoid floating
  - LEDs can be disabled in firmware during deep sleep
  - Low quiescent current regulator chosen

---

### 2. Button Inputs and Debouncing
- **Pull-ups:** Internal MCU pull-ups used where possible  
- **RC Filtering:** Small capacitors (~0.01–0.1 µF) added to buttons to suppress EMI and reduce bounce noise  
- **Software Debounce:** Firmware ensures a 20–50 ms stable input before registering a button press  
- **Routing:** Button traces kept short and away from high-current paths and SW nodes of the buck converter

---

### 3. Grounding Strategy
- **Solid Ground Plane:** Entire board uses a continuous GND plane for digital and analog return paths  
- **High-current Loops:** Buck converter input/output loop minimized to reduce noise  
- **Button and GPIO Routing:** Kept away from noisy nodes (SW, inductor) and antenna to preserve signal integrity

---

### 4. MCU & Connectivity
- **ESP32-S3-WROOM-1:** Chosen for BLE support, low-power sleep modes, and sufficient GPIO for multiple buttons  
- **UART Header:** Exposed for programming and debugging (J6)  
- **GPIO Mapping:** Each button connected to a dedicated GPIO pin (Bin1–Bin4) with pull-up resistor

---

### 5. PCB Layout Notes
- **Layering:** 2-layer PCB with top and bottom copper, ground plane on bottom  
- **Component Placement:** 
  - Decoupling capacitors close to MCU power pins
  - Buck converter and input capacitors placed to minimize high-di/dt loop area  
- **Antenna Clearance:** Kept area around ESP32 antenna free from copper to maximize RF performance  
- **Vias:** Used to connect top and bottom planes for GND continuity

---

## Files Included

- `schematics/` — KiCad schematic PDF and source file  
- `pcb/` — PCB layout images and 3D renders  
- `manufacturing/` — Gerbers, drill files, BOM (CSV)  

---

## Future Enhancements
- Battery-powered operation with Li-ion charging
- LED status indicators for battery and Bluetooth connection
- Expansion to additional buttons or rotary encoder
- Firmware implementing Bluetooth HID standard for multiple platforms

---
