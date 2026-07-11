# STM32-Learning-Notes
# Smart Temperature-Controlled Fan System (STM32F103C8T6)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-STM32-blue)](https://www.st.com/)

A dual-mode (Auto/Manual) intelligent fan control system based on STM32F103C8T6. It automatically adjusts fan speed according to ambient temperature, supports manual override via rotary encoder, and features multi-level temperature alarms with LED indicators and buzzer alerts.

---

## ✨ Features

- **Dual-Mode Control**:
  - **Auto Mode** (Temp > 25°C): Fan speed linearly increases with temperature (`Speed = Temperature`).
  - **Standby Mode** (20°C ≤ Temp ≤ 25°C): Fan stops to save energy.
  - **Manual Mode** (Temp < 20°C): User controls speed via rotary encoder (step = 4).
- **Multi-Level Alarms**:
  - **> 65°C**: Red LED on + Buzzer sounds (Central C tone via TIM2 interrupt).
  - **55°C ~ 65°C**: All LEDs off (silent warning).
  - **< 55°C**: Green LED on (safe status).
- **PWM Noise Elimination**: Adjusted timer prescaler and auto-reload to set PWM frequency to **25 kHz**, eliminating audible whining noise.
- **Real-Time Display**: OLED screen shows current motor speed and temperature value.
- **Hardware Debouncing**: Encoder input with software filtering for stable manual control.

---

## 🛠️ Hardware Requirements

| Component | Model/Pin |
| :--- | :--- |
| MCU | STM32F103C8T6 (Blue Pill) |
| Temperature Sensor | NTC Thermistor / Analog Output (ADC) |
| DC Motor | 3V~6V DC Motor with driver (MOSFET/L298N) |
| Rotary Encoder | EC11 (with push button) |
| OLED Display | 0.96" I2C OLED (SSD1306) |
| Buzzer | Passive Buzzer (PB12) |
| LEDs | Red (PA8), Green (PA9) |

---

## 🔌 Pin Mapping (Customizable)

| Peripheral | Pin | Function |
| :--- | :--- | :--- |
| Motor PWM | PAx (e.g., PA0/PA1) | PWM output for speed control |
| ADC (Temp) | PAx (e.g., PA1) | Analog voltage reading |
| Encoder CLK | PA0 | Encoder phase A |
| Encoder DT | PA1 | Encoder phase B |
| Buzzer | PB12 | Timer2 interrupt driven |
| Red LED | PA8 | Alarm indicator |
| Green LED | PA9 | Safe indicator |
| OLED SCL | PB6 | I2C Clock |
| OLED SDA | PB7 | I2C Data |

> **Note**: Actual pins depend on your `Motor.h`, `Encoder.h`, `AD.h`, and `OLED.h` definitions. Adjust according to your wiring.

---

## 🚀 How to Use

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/Smart-Temperature-Controlled-Fan-STM32.git
