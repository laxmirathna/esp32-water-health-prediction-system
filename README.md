# 💧 ESP32 Water Health Prediction System
### Edge Water Quality Guardian | Monitor • Analyze • Predict • Protect

<p align="center">
  <strong>An IoT-based intelligent water quality monitoring and prediction prototype using ESP32.</strong>
</p>

---

## 🌊 1. Project Overview

Water quality monitoring is essential for protecting human health and maintaining a clean environment. This project presents an **ESP32-based Water Health Prediction System** that monitors important water quality parameters, analyzes sensor readings, estimates future trends, and generates alerts based on predefined safety limits.

The system uses three sensors to monitor:

- **pH:** Measures the acidity or alkalinity of water.
- **TDS (Total Dissolved Solids):** Estimates the concentration of dissolved substances.
- **Turbidity:** Indicates the presence of suspended particles in water.

The ESP32 processes the sensor readings using a rule-based decision-making algorithm. It calculates a Water Health Score, identifies abnormal parameters, estimates possible future changes, and provides recommendations.

An OLED display presents the results, while LEDs and a buzzer provide visual and audible alerts.

## 🎯 2. Project Objectives

- Develop a real-time water quality monitoring system.
- Monitor pH, TDS, and turbidity simultaneously.
- Analyze sensor readings using an ESP32 microcontroller.
- Estimate future water quality trends using stored readings.
- Calculate a water health score based on predefined thresholds.
- Identify abnormal water quality parameters.
- Generate early warnings and recommendations.
- Provide an interactive monitoring interface using an OLED display.

## ✨ 3. Key Features

| Feature | Description |
|---|---|
| Real-Time Monitoring | Continuously reads three water quality sensors. |
| Trend Detection | Identifies increasing, decreasing, and stable readings. |
| History-Based Prediction | Estimates future values using recent sensor readings. |
| Water Health Score | Calculates a score out of 100. |
| Status Classification | Categorizes water as Excellent, Good, Moderate, Poor, or Unsafe. |
| Risk Analysis | Assigns LOW, MEDIUM, or HIGH risk levels. |
| Responsible Parameter | Identifies the parameter with the largest deviation from its programmed limit. |
| OLED Interface | Displays live readings, predictions, and decisions. |
| Alert System | Uses three LEDs and a buzzer to indicate water status. |

## 🔧 4. Hardware Components

| Component | Purpose |
|---|---|
| ESP32 Development Board | Main processing and control unit |
| pH Sensor | Measures water pH |
| TDS Sensor | Measures dissolved solids |
| Turbidity Sensor | Measures water clarity |
| SSD1306 OLED Display | Displays sensor readings and results |
| Green LED | Indicates Excellent or Good status |
| Yellow LED | Indicates Moderate or Poor status |
| Red LED | Indicates Unsafe status |
| Buzzer | Generates audible alerts |
| Breadboard and Jumper Wires | Circuit connections |
| 220Ω Resistors | LED current limiting |

## 🔌 5. Hardware Connections

The system uses the following ESP32 GPIO configuration.

| Module | Signal | ESP32 GPIO |
|---|---|---|
| pH Sensor | Analog Output | GPIO34 |
| TDS Sensor | Analog Output | GPIO35 |
| Turbidity Sensor | Analog Output | GPIO32 |
| OLED | SDA | GPIO21 |
| OLED | SCL | GPIO22 |
| Green LED | Anode through 220Ω | GPIO18 |
| Yellow LED | Anode through 220Ω | GPIO19 |
| Red LED | Anode through 220Ω | GPIO5 |
| Buzzer | Positive | GPIO23 |

### Power Connections

- ESP32 3.3V → Breadboard positive rail.
- ESP32 GND → Breadboard negative rail.
- All sensor VCC pins → Positive rail.
- All sensor GND pins → Negative rail.
- OLED VCC → 3.3V.
- OLED GND → GND.
- LED cathodes → GND.
- Buzzer negative → GND.



## 🖥️ 6. Wokwi Circuit Simulation

The complete circuit is designed using a Wokwi-style ESP32 setup to represent the sensor connections, OLED interface, and alert system.

The simulation design includes:

- ESP32 development board
- pH, TDS, and turbidity sensor modules
- SSD1306 OLED display
- Three status LEDs
- Buzzer
- Breadboard power distribution
- GPIO-based signal connections

### Wokwi Circuit Diagram

![ESP32 Water Health Prediction Wokwi Circuit](<img width="1536" height="1024" alt="ESP32 Water Health Prediction Diagram" src="https://github.com/user-attachments/assets/667e3a48-f598-45f9-b2b9-97860bebfb9b" />
)


## ⚙️ 7. Working Principle

The project operates through the following processing stages:

**Stage 1 – Sensor Data Acquisition**

The ESP32 reads analog signals from GPIO34, GPIO35, and GPIO32.

**Stage 2 – Sensor Value Conversion**

Raw ADC values are converted into estimated pH, TDS, and turbidity values.

**Stage 3 – Trend Detection**

The current sensor values are compared with previously recorded values to identify changes.

**Stage 4 – History-Based Prediction**

The system stores five readings for each parameter and calculates their averages. It uses the difference between the current value and the average to estimate future values.

**Stage 5 – Water Health Evaluation**

Each parameter is checked against its programmed safety threshold. A health score is calculated based on the results.

**Stage 6 – Risk Analysis**

Predicted values are checked to identify possible risks.

**Stage 7 – Decision and Recommendation**

The system identifies abnormal parameters and generates suitable recommendations.

**Stage 8 – Output and Alerts**

The OLED displays the results, the Serial Monitor prints detailed information, and LEDs and the buzzer indicate the water status.

## 📊 8. Water Quality Decision Algorithm

The program uses the following thresholds:

| Parameter | Programmed Safe Range |
|---|---|
| pH | 6.5 – 8.5 |
| TDS | ≤ 300 ppm |
| Turbidity | ≤ 5 NTU |

### Water Health Score

The scoring mechanism assigns points based on the three parameter checks.

| Parameter | Score |
|---|---:|
| pH within range | 33 |
| TDS within range | 33 |
| Turbidity within range | 34 |
| **Maximum Score** | **100** |

### Water Status Classification

| Score | Status |
|---|---|
| 90–100 | Excellent |
| 75–89 | Good |
| 60–74 | Moderate |
| 40–59 | Poor |
| Below 40 | Unsafe |

### Risk Classification

The predicted sensor values determine the risk level:

- **LOW:** No predicted parameter violates its programmed threshold.
- **MEDIUM:** One predicted parameter violates its threshold.
- **HIGH:** Two or more predicted parameters violate their thresholds.

## 🔮 9. Prediction and Analysis

The system implements a simple history-based prediction technique.

It stores the last five sensor readings in arrays and calculates their averages.

The prediction formula used is:

`Predicted Value = Current Value + (Current Value - Average of Previous Five Readings)`

This method estimates the direction and magnitude of a possible change using recent readings.

### Trend Detection

| Condition | Detected Trend |
|---|---|
| Current value > Previous value | Increasing |
| Current value < Previous value | Decreasing |
| Current value = Previous value | Stable |

### Responsible Parameter Identification

The system evaluates how far each current reading deviates from its programmed safe limit.

It identifies the parameter with the largest deviation and generates a corresponding reason:

- pH → pH outside safe range.
- TDS → High dissolved solids.
- Turbidity → High suspended particles.
- None → All parameters normal.

**Note:** This is a rule-based prediction and decision system, not a trained machine-learning model.

## 📟 10. OLED Display Interface

The SSD1306 OLED display is configured with four information pages.

| Page | Information Displayed |
|---|---|
| Page 1 | Live pH, TDS, and turbidity readings |
| Page 2 | Water health score and status |
| Page 3 | Predicted values, risk level, and early warning |
| Page 4 | Responsible parameter and recommended action |

Each page is intended to appear for approximately three seconds.

📌 **OLED Display Output:**

![OLED Display](Images/oled_display.png)

## 🚨 11. Alert System

The system provides visual and audible alerts depending on the calculated water status.

| Water Status | LED | Buzzer |
|---|---|---|
| Excellent | Green | OFF |
| Good | Green | OFF |
| Moderate | Yellow | OFF |
| Poor | Yellow | 1000 Hz short alert |
| Unsafe | Red | 2000 Hz continuous tone |

This helps users identify abnormal conditions without continuously monitoring the display.

## 🖼️ 12. Project Output

The system provides two primary output interfaces:

**OLED Display**
- Live sensor readings.
- Water health score.
- Status classification.
- Predicted sensor values.
- Risk analysis and recommendations.

**Serial Monitor**
- Detailed sensor readings.
- Health score and status.
- Detected problems.
- Recommendations.
- Trends and predicted values.
- Early warnings.
- Responsible parameter and reason.

📌 **Serial Monitor Output:**

![Serial Monitor Output](Images/serial_monitor.png)


## 💻 13. Software Requirements

- Arduino IDE
- ESP32 Board Package
- C/C++ (Arduino Framework)
- Wokwi Simulation Platform

### Required Libraries

1. `Wire.h`
2. `Adafruit_GFX.h`
3. `Adafruit_SSD1306.h`

### Uploading the Program

1. Install Arduino IDE.
2. Install the ESP32 board package.
3. Install the required Adafruit libraries.
4. Open the `.ino` source file.
5. Select the appropriate ESP32 board and COM port.
6. Upload the program.
7. Open Serial Monitor at 115200 baud.
8. Verify the sensor readings and output indicators.

The OLED is configured with I²C address `0x3C`.

## 📁 14. Project Repository Structure

```text
ESP32-Water-Health-Prediction/
│
├── README.md
│
├── Code/
│   └── Water_Health_Prediction.ino
│
├── Hardware_Connections/
│   ├── Hardware_Connections.pdf
│   └── Pin_Configuration.png
│
└── Images/
    ├── wokwi_circuit.png
    ├── hardware_setup.png
    ├── oled_display.png
    └── serial_monitor.png
```

The repository is organized to keep source code, hardware documentation, and visual references separate for easier understanding and maintenance.

## ⚠️ 15. Limitations

- Sensor conversion formulas require calibration with actual sensor modules.
- The initial history arrays contain zeros, which can affect early predictions.
- The first trend comparison uses zero-initialized previous values.
- The current OLED page-management logic can produce a blank fifth page and should be corrected.
- The prediction method is a simple extrapolation technique.
- The system monitors only three water quality parameters.
- The current implementation does not include cloud connectivity or a trained AI model.

**Important:** This is an educational monitoring prototype. pH, TDS, and turbidity readings alone cannot establish that water is safe to drink. The system does not detect pathogens, heavy metals, or all chemical contaminants. Its output must not be treated as drinking-water certification.

## 🚀 16. Future Enhancements

- Integrate machine-learning models for more advanced water quality prediction.
- Add Wi-Fi connectivity for remote monitoring.
- Develop an IoT dashboard for historical data visualization.
- Integrate cloud-based data storage.
- Add temperature and dissolved oxygen sensors.
- Improve sensor calibration and prediction accuracy.
- Introduce automated water filtration control.
- Develop a mobile application for real-time notifications.

## 🌱 17. Applications

- Smart water monitoring systems.
- Educational IoT and embedded systems projects.
- Environmental monitoring.
- Agriculture and irrigation monitoring.
- Water quality awareness and demonstration systems.

## 👩‍💻 18. Conclusion

The **ESP32 Water Health Prediction System – Edge Water Quality Guardian** demonstrates the integration of embedded systems, sensor interfacing, data processing, rule-based prediction, and alert mechanisms.

By combining multiple water quality sensors with an ESP32 microcontroller, the project provides a practical prototype for monitoring selected water parameters and identifying potential changes.

The system demonstrates how IoT and embedded technologies can contribute to smarter environmental monitoring and water quality awareness.

---

### 💙 Clean Water. Healthy Life.

**Project Domain:** Embedded Systems | IoT | Water Quality Monitoring | Sensor Data Analysis

**Controller:** ESP32

**Simulation Platform:** Wokwi

**Programming Language:** Embedded C/C++ (Arduino Framework)
