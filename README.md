# 🌤️ ESP32 Weather Station

### ESP32 + Blynk IoT + OpenWeather API + DHT11 + Light Sensor + I2C LCD

This project is a complete IoT **Weather Monitoring System** using an ESP32.
It collects **indoor temperature/humidity**, **ambient light**, and **outdoor weather data** (via OpenWeather API), displays them on an **I2C LCD**, and uploads everything to the **Blynk IoT App**.

---

## 📸 Project Overview

Features:

* 🌡️ Indoor temperature & humidity (DHT11)
* 💡 Light sensor reading (LDR analog)
* ☁️ Outdoor weather from OpenWeather API
* 📟 16×2 I2C LCD display
* 📱 Blynk IoT Virtual Pin dashboard
* ♻️ Automatic WiFi reconnect
* 🌐 JSON parsing using ArduinoJson
* ⏱ Weather update every 10 minutes

---

## 🛠️ Hardware Required

| Component                                      | Qty |
| ---------------------------------------------- | --- |
| ESP32 Dev Board                                | 1   |
| DHT11 Sensor                                   | 1   |
| Light Sensor (LDR + resistor OR analog module) | 1   |
| 16×2 I2C LCD (0x27)                            | 1   |
| Jumper Wires                                   | —   |

---

## 🔌 Wiring Diagram

### ESP32 Connections

| Component       | ESP32 Pin |
| --------------- | --------- |
| DHT11 Data      | GPIO 5    |
| Light Sensor AO | GPIO 32   |
| LCD SDA         | GPIO 21   |
| LCD SCL         | GPIO 22   |

Notes:

* Use **ADC1 pins only** (32, 33, 34, 35, 36, 39) for analogRead when WiFi is ON.
* Light sensor must be **3.3V compatible**.

---

## 📱 Blynk Virtual Pins

| Virtual Pin | Data                    |
| ----------- | ----------------------- |
| V0          | Cloud Cover (%)         |
| V1          | Outdoor Temperature     |
| V2          | Outdoor Humidity        |
| V3          | Indoor Temperature      |
| V4          | Indoor Humidity         |
| V5          | Light Level (ADC Value) |

---

## 🌍 OpenWeather API

The project fetches real-time outdoor weather:

```
https://api.openweathermap.org/data/2.5/weather?lat=5.36&lon=100.32&appid=YOUR_API_KEY&units=metric
```

Replace:

* `lat=` → your latitude
* `lon=` → your longitude
* `appid=` → your API key

---

## 📄 Code (Included in repo)

Your main `.ino` file contains:

* WiFi + Blynk setup
* JSON parsing with ArduinoJson
* LCD updates
* DHT11 data reading
* Light sensor reading
* HTTP GET request to OpenWeather
* Timer-based updates

---

## 🛠️ Required Libraries

Install via **Arduino Library Manager**:

```
Blynk
DHT11
ArduinoJson
LiquidCrystal_I2C
WiFi
HTTPClient
BlynkSimpleEsp32
```

---

## ▶️ How to Use

1. Update WiFi credentials:

   ```cpp
   const char* ssid = "YOUR_WIFI";
   const char* pass = "YOUR_PASSWORD";
   ```

2. Insert your:

   * **Blynk Auth Token**
   * **OpenWeather API Key**

3. Upload to ESP32.

4. Open Serial Monitor at **115200 baud**.

5. Open the Blynk app to see live data.

---

## 🕒 Update Intervals

Weather updates every **10 minutes**:

```cpp
timer.setInterval(600000L, getOpenWeather);
```

Local sensor values update every **1 second**.

---

## ⭐ Future Improvements

* Add real-time graphing in Blynk
* Add barometric pressure (BMP280)
* Add OLED version
* Store logs on SD card
* Add auto brightness for LCD

---

## 📜 License

This project is open-source and free to modify.

---
