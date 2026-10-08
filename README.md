# 🔐 Smart Door Lock System Using STM32

### Password-Based Access Control with Timed Security Lockout

A password-based smart door lock system developed using the **STM32F103C8T6 Blue Pill** and simulated using **Wokwi**.

The system uses a **4×4 keypad** for password entry, a **16×2 LCD** for user feedback, a **servo motor** to control the door lock, and a **piezo buzzer** to provide a security alert after multiple incorrect password attempts.

---

## 📌 Project Overview

Traditional mechanical locks can be lost, duplicated, or physically compromised. This project demonstrates a simple electronic access-control system using a microcontroller.

The user enters a password through a keypad. If the password is correct, the servo motor unlocks the door. If an incorrect password is entered three consecutive times, the system activates a security alarm and disables keypad input for **5 minutes**.

The complete system is implemented as a **software-based embedded-system simulation** using Wokwi.

---

## ✨ Features

- 🔢 Password-based authentication
- 🔐 4×4 matrix keypad
- 📟 16×2 LCD user interface
- 🔓 Servo-controlled door locking mechanism
- ❌ Incorrect password detection
- 🚨 Three-attempt security protection
- 🔊 Three-beep buzzer alarm
- ⏱️ 5-minute automatic lockout
- ⏳ Real-time lockout countdown
- 🔄 Automatic door relocking
- 🖥️ STM32 HAL-based Embedded C implementation
- 🧪 Fully simulated using Wokwi

---

## 🛠️ Hardware Components

| Component | Description |
|---|---|
| STM32F103C8T6 | Main microcontroller |
| 4×4 Matrix Keypad | Password input |
| 16×2 LCD (LCD1602) | User interface |
| Servo Motor | Door lock mechanism |
| Piezo Buzzer | Security alarm |
| Power Supply | Component power |

> The hardware is represented and tested through simulation in Wokwi.

---

## 💻 Software & Tools

- **STM32CubeIDE**
- **STM32CubeMX**
- **Embedded C**
- **STM32 HAL Library**
- **Wokwi Simulator**
- **STM32F1 Firmware Package**

---

# 🔌 Pin Configuration

## 4×4 Keypad

| Keypad Pin | STM32 Pin |
|---|---|
| R1 | PA0 |
| R2 | PA1 |
| R3 | PA2 |
| R4 | PA3 |
| C1 | PA4 |
| C2 | PA5 |
| C3 | PA6 |
| C4 | PA7 |

---

## 📟 16×2 LCD

| LCD Pin | STM32 Pin |
|---|---|
| RS | PB0 |
| E | PB1 |
| D4 | PB5 |
| D5 | PB6 |
| D6 | PB7 |
| D7 | PB8 |
| RW | GND |
| VSS | GND |
| VDD | 5V |
| V0 | GND |
| A | 5V |
| K | GND |

The LCD operates in **4-bit mode**, so D0–D3 are not used.

---

## 🔓 Servo Motor

| Servo Pin | STM32 / Supply |
|---|---|
| PWM | PA8 / TIM1_CH1 |
| V+ | 5V |
| GND | GND |

The servo is controlled using the **TIM1 PWM peripheral**.

---

## 🔊 Buzzer

| Buzzer Pin | STM32 / Supply |
|---|---|
| Positive | PB9 / TIM4_CH4 |
| Negative | GND |

The buzzer is driven using **TIM4 PWM**.

---

# 🔄 System Working

```text
                    ┌─────────────────┐
                    │      START      │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │  Enter Password │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │  Keypad Input   │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Password Correct?│
                    └──────┬─────┬────┘
                           │ YES │ NO
                           ↓     ↓
                   ┌──────────┐  ┌─────────────┐
                   │  Unlock  │  │  Incorrect  │
                   │   Door   │  │  Password   │
                   └────┬─────┘  └──────┬──────┘
                        ↓                ↓
                   ┌──────────┐    Attempts = 3?
                   │ 3 Second │         │
                   │  Delay   │      ┌──┴───┐
                   └────┬─────┘     NO     YES
                        ↓             │       │
                   ┌──────────┐       ↓       ↓
                   │  Relock  │     Retry  ┌────────────┐
                   │   Door   │            │Buzzer Alarm│
                   └──────────┘            └─────┬──────┘
                                                  ↓
                                          ┌──────────────┐
                                          │System Locked │
                                          │    05:00     │
                                          └──────┬───────┘
                                                 ↓
                                          ┌──────────────┐
                                          │ 5 Minute     │
                                          │ Countdown    │
                                          └──────┬───────┘
                                                 ↓
                                          ┌──────────────┐
                                          │ Reset System │
                                          └──────────────┘
