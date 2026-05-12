# 🌀 TCL Air Conditioner Integration for Home Assistant

Note: I modified sorz's code to work with my Rovsun unit. 
EN Translated with Google – successfully tested with **Rovsun TSC-09HA1/I3XI22B-I (indoor) & TSC-09HA1/I3XI22B-O (outdoor) **
Simple DIY project with ESP32 + USB cable. No cloud required.

---

## 🛠️ What you need

- **ESP32** (e.g., ESP32-C3, WROOM32, NodeMCU)
- **USB-A connector or cable**
👉 I used this one: [AliExpress link](https://www.aliexpress.com/item/1005005776162012.html)
- **Home Assistant with ESPHome (version 2023.3.0 or later)**

---

## 🔌 Wiring

| USB-A Pin | Wire Color | → ESP32 Pin |
|-----------|------------|--------------|
| GND       | Black      | VIN/VCC      |
| D+        | Green      | GND          |
| D-        | Gray       | RXD          |
| VBUS      | Red        | TXD          |

### 🔍 Example images
(Note that I haven't paid attention to the cable colors here. However, the colors in the table generally correspond to standard USB-A cables that can be easily cut.)

<img src="https://github.com/user-attachments/assets/9b674e06-41ca-4bcf-b09b-691a5fbd8545" width="400"/>
<br/>

![Wiring Example 2](https://github.com/user-attachments/assets/e30fadd9-19cd-47ec-baab-86f8a80410f6)

![7480a856c7839044d7a04292d352b709a2155c07_2_296x500](https://github.com/user-attachments/assets/5b3ccbb8-eb62-4743-8d05-f88a9b986743)

---

## 🧠 Setup in Home Assistant

> This solution is based on **ESPHome** and only works with Home Assistant.

### 1. Install ESPHome

- In Home Assistant, go to **Settings → Add-ons → ESPHome** and install it.

### 2. Create a new device

- In the ESPHome dashboard → "New Device"
- Select your ESP32 type, e.g., `esp32-c3-devkitm-1` or `nodemcu-32s`

### 3. Insert the configuration

#### Option A: Simple configuration
[📄 Sample_conf.yaml](https://github.com/sorz2122/tclac/blob/master/Sample_conf.yaml)

#### Option B: Advanced configuration
[📄 TCL-Conditioner.yaml](https://github.com/sorz2122/tclac/blob/master/TCL-Conditioner.yaml)

📝 **Important:**
- Adjust Wi-Fi credentials, device name, etc.
- Comments in the YAML file will help with the setup.

### 4. Flash to ESP32

- Connect via USB cable or use OTA (Over-the-Air)

---

## ✅ Compatible Air Conditioners

These models have been successfully tested:

- Rovsun TSC-09HA1/I3XI22B-I (indoor) & TSC-09HA1/I3XI22B-O (outdoor)
- ...and similar models

⚠️ **Note:**
Even if the model name matches, there may be differences (no USB port, no UART on the board, etc.). ---

## ☕ Support

https://buymeacoffee.com/sorz2122

<img src="https://github.com/user-attachments/assets/87d5d62f-ba5c-4a7e-a4b8-4cf1fd3018af" width="400"/>
<br/>

---

## 🔧 Advanced Configuration via Remote Package

You can load the configuration modularly:

```yaml
packages:
  remote_package:
    url: https://github.com/sorz2122/tclac.git
    ref: master
    files:
      - packages/core.yaml   # Main module
      # - packages/leds.yaml # Optional
    refresh: 30s
