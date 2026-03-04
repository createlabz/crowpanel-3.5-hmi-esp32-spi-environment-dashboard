# 🌡️ CrowPanel 3.5" HMI ESP32 Environmental Monitoring Dashboard  
### LVGL + DHT11 + Bluetooth Serial

An **LVGL-based environmental monitoring dashboard** built for the  
**CrowPanel 3.5"-HMI ESP32 Display (480×320 SPI TFT LCD Resistive Touch)** using **Arduino IDE**.

This project reads **temperature and humidity data from a DHT11 sensor**, visualizes it using **LVGL widgets (charts, gauges, and indicators)**, and transmits the readings through **Bluetooth Serial (SPP)**. The screen backlight can also be controlled remotely via Bluetooth commands.

The display uses a **resistive touch panel**, which requires **pure manual calibration**.

---

# 📺 Hardware Used

### 🖥 Display Board
**CrowPanel 3.5"-HMI ESP32 Display**

Specifications:

- Screen Size: **3.5 inch**
- Resolution: **480 × 320**
- Display Interface: **SPI**
- Touch Type: **Resistive Touch**
- Compatible with:
  - Arduino
  - LVGL
  - PlatformIO
  - MicroPython

---

### 🌡 Sensor
**DHT11 Temperature and Humidity Sensor**

Used to measure:

- Temperature  
- Humidity  

---

### 📡 Communication

**Bluetooth Serial (SPP)**

Used for:

- Remote monitoring of sensor values
- Sending commands to control the display backlight

---

# 🧰 Software Versions (Tested)

| Component | Version |
|-----------|--------|
| Arduino IDE | **2.3.7** |
| ESP32 Board Package | **2.0.17 (Espressif Systems)** |
| LVGL | **8.3.11** |
| TFT_eSPI | **2.5.43 (Bodmer)** |
| DHT Sensor Library | **Latest Version** |

---

# 📦 LVGL Library Used

This project uses **LVGL version 8.3.11**.

If the LVGL library used in this project is uploaded in this repository, you can download it here: 

*(Insert the repository link once uploaded.)*

---

# ✨ Project Features

✔ LVGL graphical dashboard  
✔ Temperature and humidity monitoring  
✔ Real-time UI updates  
✔ Bluetooth Serial communication  
✔ Bluetooth commands to control the screen backlight  
✔ Full-screen LVGL rendering using **PSRAM**  
✔ Resistive touch interaction  
✔ Manual touch calibration  

---

# 🔌 Hardware Wiring

## DHT11 Sensor Connection

| DHT11 Pin | ESP32 Pin |
|-----------|-----------|
| VCC | 3.3V |
| GND | GND |
| DATA | **GPIO 32** |

⚠ If using a **bare DHT11 sensor**, add a **10K pull-up resistor** between **DATA and VCC**.

---

# 🖐 Touch Screen Type

The CrowPanel display uses a **Resistive Touch Screen**.

### Characteristics

- Requires **manual calibration**
- Works with **pressure-based input**
- Can be used with **finger or stylus**
- Less sensitive compared to capacitive touch screens

---

# 🎯 Touch Calibration

This project uses manual calibration values:

```cpp
uint16_t calData[5] = {292, 3607, 302, 3486, 7};

Applied using: tft.setTouch(calData);

--------------------------------------------------------------------

📚 Required Libraries

Install the following libraries using Arduino Library Manager.

LVGL

Version 8.3.11

TFT_eSPI

Version 2.5.43

DHT Sensor Library

Install:

DHT sensor library by Adafruit

Adafruit Unified Sensor


--------------------------------------------------------------------

⚙ Arduino IDE Configuration

Set the following in Tools:

| Setting         | Value            |
| --------------- | ---------------- |
| Board           | ESP32 Dev Module |
| Flash Frequency | 80 MHz           |
| Upload Speed    | 921600           |
| PSRAM           | **Enabled**      |

--------------------------------------------------------------------

🖥 TFT_eSPI Configuration

You must configure TFT_eSPI to match the CrowPanel display.

Open the following file:

Arduino/libraries/TFT_eSPI/User_Setup_Select.h

Enable the configuration that matches your CrowPanel 3.5" SPI display.

Incorrect configuration may cause:

White screen

Incorrect colors

Touch not working

--------------------------------------------------------------------

🧠 LVGL Frame Buffer

The project allocates a full display buffer in PSRAM for smoother rendering.

buf1 = (lv_color_t *)heap_caps_malloc(
screenWidth * screenHeight * sizeof(lv_color_t),
MALLOC_CAP_SPIRAM
);

If PSRAM allocation fails, the program will display:

PSRAM allocation failed!

--------------------------------------------------------------------

🎨 Customizing the UI Design

This project loads the LVGL Widgets Demo UI:

lv_demo_widgets();

If you want to change the design, layout, or widgets, you can modify the LVGL demo source file.

Open the following file:

C:\Users\User\Documents\Arduino\libraries\lvgl\src\demos\widgets\lv_demo_widgets.c

Inside this file you can customize:

Layouts

Charts

Gauges

Panels

Colors

UI widgets

Sensor display elements

This allows you to fully redesign the interface or create your own dashboard UI.

--------------------------------------------------------------------


📲 Bluetooth Serial

The ESP32 creates a Bluetooth device named:

CrowPanel_Control

You can connect using:

Android Bluetooth Terminal apps

PC Bluetooth Serial tools

Any Bluetooth SPP terminal

--------------------------------------------------------------------

📡 Bluetooth Commands
Command	Function
ON	Turn screen backlight ON
OFF	Turn screen backlight OFF

Backlight control pin:

GPIO 27

--------------------------------------------------------------------

📊 Example Output

Bluetooth output example:

Temp:29C  Hum:65%

Sensor values update approximately every 2 seconds.

--------------------------------------------------------------------

🔁 Program Workflow

The program performs the following sequence:

1️⃣ Initialize Serial communication
2️⃣ Initialize Bluetooth Serial
3️⃣ Start DHT11 sensor
4️⃣ Initialize TFT display using TFT_eSPI
5️⃣ Initialize LVGL graphics engine
6️⃣ Allocate LVGL frame buffer in PSRAM
7️⃣ Start LVGL timer interrupt
8️⃣ Load LVGL widgets demo UI
9️⃣ Read temperature and humidity every 2 seconds
🔟 Send sensor data through Bluetooth


--------------------------------------------------------------------

🚀 Upload Instructions

1️⃣ Connect the CrowPanel to your computer via USB
2️⃣ Open the project in Arduino IDE
3️⃣ Select the correct COM port
4️⃣ Compile and upload the sketch
5️⃣ Open Serial Monitor (115200 baud)

After uploading, the LVGL dashboard should appear on the screen.

--------------------------------------------------------------------

🛠 Troubleshooting
PSRAM allocation failed

Enable PSRAM in Arduino IDE settings (Tools).

--------------------------------------------------------------------

White screen

Check TFT_eSPI configuration.

--------------------------------------------------------------------

Touch not accurate

Recalibrate the touch panel and update:

tft.setTouch(calData);

--------------------------------------------------------------------

Bluetooth not appearing

Ensure the ESP32 board supports Bluetooth Classic (SPP).

--------------------------------------------------------------------

# 🔮 Possible Improvements

The current project already includes **real-time LVGL charts that update with live sensor data** from the DHT11. Future upgrades may include:

🌫 Air quality sensors (MQ135, BME680, SGP30)  
📡 WiFi cloud monitoring (MQTT / IoT dashboards)  
📁 SD card data logging for historical data  
📱 Mobile monitoring applications

--------------------------------------------------------------------

📜 License

MIT License

--------------------------------------------------------------------

👨‍💻 Author

Developed for experimentation and UI development using:

CrowPanel ESP32 Displays + LVGL dashboards

--------------------------------------------------------------------

⭐ If this project helped you, consider giving the repository a star!

