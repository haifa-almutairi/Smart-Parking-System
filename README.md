# Smart Parking System

A Smart Parking System that integrates **embedded systems**, **sensing technologies**, and **cloud-based communication** to improve parking efficiency and automation. 
The system uses a dual-controller architecture an **ESP32-based monitoring subsystem** and an **Arduino-based mechanical control subsystem** combined with a **Firebase-powered web dashboard** for real-time monitoring and booking.

---

## Overview

Traditional parking systems rely on manual monitoring and static space allocation, leading to congestion and inefficiency. This project solves that by:

- Authenticating **employees** via RFID cards for fully automated entry/parking/retrieval.
- Letting **visitors** book parking slots in advance through a web dashboard.
- Using **ultrasonic sensors** to detect real-time slot occupancy.
- Synchronizing physical and digital parking states via **Firebase Realtime Database**.
- Mechanically parking/retrieving vehicles using a **stepper-motor-driven attachment system**.

---

## Features

| Feature | Description |
|---|---|
| 🔑 RFID Employee Access | Employees scan an RFID card to automatically open the gate and trigger parking/retrieval |
| 📡 Real-Time Slot Monitoring | Ultrasonic sensors detect vehicle presence and update status instantly |
| ☁️ Firebase Integration | Live sync between hardware and web dashboard |
| 🖥️ Web Dashboard | Visitors view slot availability and make reservations |
| 💳 Simulated Payment | Mock payment flow for booking confirmation (no real transactions) |
| 📜 Booking History | Users can view past and current reservations |
| 🤖 Chatbot Assistant | Simple guided help for booking and slot color meaning |
| 🛡️ Admin Panel | Monitor all bookings and system activity |
| 🔥 Safety Monitoring | MQ-2 gas/smoke sensor with buzzer alerts |
| 📈 Scalable Design | 4 physical slots, 8 supported in software |

---

## Hardware Components

| Component | Quantity | Role |
|---|---|---|
| ESP32 | 1 | Sensor monitoring + Firebase communication |
| Arduino Uno R3 | 1 | Mechanical control (motors, RFID, servo, buzzer) |
| HC-SR04 Ultrasonic Sensors | 4 | Detect vehicle presence per slot |
| RC522 RFID Reader | 1 | Employee authentication |
| Stepper Motors | 2 | Horizontal & vertical attachment movement |
| DM542 Stepper Drivers | 2 | Drive the main stepper motors |
| Servo Motor | 1 | Gate control |
| MQ-2 Gas/Smoke Sensor | 1 | Safety monitoring |
| Limit Switches | 2 | Axis calibration & boundary detection |
| LCD Display (16x2, I2C) | 1 | Real-time slot info display |
| Buzzer | 1 | Audio alerts |
| ULN2003 Driver Board | 1 | Secondary stepper motor signal monitoring |
| Power Supply | 1 (24V/5V) | Power for motors and logic components |
| Power Bank | 1 | Backup power |

> ⚡ **Voltage Note:** The ESP32 uses 3.3V logic while the HC-SR04 ECHO pin outputs 5V — a **voltage divider or level shifter** is required between them. All components share a **common ground**.

---

## Software Stack

| Tool | Purpose |
|---|---|
| **Arduino IDE** | Programming Arduino R3 and ESP32 |
| **Firebase Realtime Database** | Cloud storage for slots, bookings, users |
| **HTML / CSS / JavaScript** | Web dashboard frontend |
| **ESP32 Local Web Server** | Local hosting of monitoring interface |

---

## Pin Connections

### ESP32 (Ultrasonic Sensors)

| Slot | TRIG | ECHO |
|---|---|---|
| 1 | GPIO 4 | GPIO 32 |
| 2 | GPIO 5 | GPIO 33 |
| 3 | GPIO 18 | GPIO 25 |
| 4 | GPIO 19 | GPIO 26 |

**LCD (I2C):** SDA → GPIO 21, SCL → GPIO 22

### Arduino Uno (Mechanical Control)

| Component | Pin |
|---|---|
| RFID SDA/SS | D10 |
| RFID RST | D9 |
| Servo (Gate) | D3 |
| Buzzer | D8 |
| MQ-2 Sensor | D7 |
| Limit Switch 1 (Rotation) | D2 |
| Limit Switch 2 (Vertical) | D5 |
| Stepper 1 DIR / STEP | A0 / A1 |
| Stepper 2 DIR / STEP | A2 / A3 |
| ULN2003 IN1–IN4 | D4, D6, A4, A5 |


---

## Web Dashboard

The dashboard includes:

1. **Login / Sign-Up** — basic credential-based auth
2. **Parking Dashboard** — grid view of up to 8 slots (Available / Occupied / Booked)
3. **Booking & Simulated Payment** — pick a time slot, enter mock payment info
4. **Booking History** — view past/current reservations
5. **Chatbot Assistant** — quick help on booking & slot colors
6. **Admin Panel** — view all bookings and system activity (monitoring only, no approval/edit)

**Slot Color Legend:** 🟩 Available · 🟥 Occupied · 🟨 Booked

---

## Use Cases & Actors

| Actor | Use Cases |
|---|---|
| **Employee** | Scan RFID card · Initiate parking · Initiate retrieval |
| **Visitor** | View slot availability · Reserve slot · Confirm booking (simulated payment) · View booking history · Chatbot assistance |
| **Administrator** | Monitor system · View bookings |
| **System** | Update parking status (ESP32) · Control mechanical system (Arduino) |

---

## Security Features

- RFID-based access control for employees
- Basic login authentication for visitors/admins
- Restricted admin panel access
- Secured local Wi-Fi network for ESP32 ↔ Firebase communication
- Ultrasonic-based collision avoidance
- MQ-2 fire/smoke detection with buzzer alert
- Limit-switch-based mechanical safety calibration

---

## Risk Assessment

| Risk | Mitigation |
|---|---|
| Network failure | Stable/secured Wi-Fi, controlled environment |
| Hardware malfunction | Regular testing & calibration |
| Power failure | Reliable power source + backup (power bank) |
| Data inaccuracy | Continuous sync & validation |
| Wi-Fi credential exposure | Secure credential storage, restricted access |
| Stepper motor / calibration errors | Sensor feedback, auto-calibration routines |
| Lack of ESP32–Arduino integration | Planned future serial communication |


---

## Standards Followed

- **IEC 61508** – Functional Safety
- **IEC 60204-1** – Electrical Safety
- **IEEE 802.11** – Wi-Fi Communication
- **ISO 9241** – Usability
- **OWASP Top Ten** – Web Security Awareness

---

## Future Work

- Mobile application for booking on the go
- Multi-floor expansion with vertical movement systems
- Reduced Wi-Fi dependency / improved connectivity reliability
- Stronger encryption for ESP32–Firebase–web communication
- Performance optimization for faster real-time updates
- Intelligent slot recommendation based on usage prediction
- Direct ESP32–Arduino communication for booking-triggered automation

