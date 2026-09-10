# BattleGuard: Advanced Military Access Control and Authentication System Using RFID and CAN Communication

## 📌 Project Overview

**BattleGuard** is a multi-node embedded access-control and authentication system designed for secure entry management in restricted areas.

The system uses **RFID authentication, CAN communication, GSM notification, LCD monitoring, LED/buzzer indication, and servo-based gate control**.

The project is implemented using **LPC2129 ARM7 microcontrollers**, with separate controller nodes handling RFID authentication, status indication, and automated gate control.

This project demonstrates practical implementation of:

- Embedded C
- ARM7 LPC2129
- UART Communication
- CAN Communication
- RFID Interfacing
- GSM Communication
- PWM
- Servo Motor Control
- LCD Interfacing
- GPIO
- Multi-node Embedded System Design

---

## 📝 Abstract

Security and controlled access are important requirements in restricted and sensitive environments. Manual verification can be time-consuming and may lead to unauthorized access.

**BattleGuard** is an automated RFID-based access-control system developed using multiple LPC2129 microcontroller nodes. An RFID reader scans the identification tag and sends the received data to the first controller through UART. The controller compares the scanned ID with a predefined authorized ID.

Based on the authentication result, a CAN message is transmitted to the other controller nodes.

For an authorized RFID tag, the gate-control node operates a servo motor to open the gate for a predefined period and then closes it automatically.

For an unauthorized RFID tag, the gate remains closed while the LCD displays the access status and the LED and buzzer provide an alert indication. A GSM module can also be used to send an SMS notification for unauthorized access.

The project demonstrates **distributed embedded control using CAN communication**.

---

## 🎯 Objectives

- Implement RFID-based authentication.
- Read RFID data using UART.
- Compare the scanned RFID with an authorized ID.
- Transfer authentication status using CAN communication.
- Control a servo motor using PWM.
- Display system status using a 20×4 LCD.
- Provide LED and buzzer indications for unauthorized access.
- Send GSM notifications for unauthorized access.
- Demonstrate multi-node communication using LPC2129.

---

## 🏗️ System Architecture

```text
                         ┌───────────────────┐
                         │     RFID TAG      │
                         └─────────┬─────────┘
                                   │
                                   ▼
                         ┌───────────────────┐
                         │   EM-18 RFID      │
                         │      READER       │
                         └─────────┬─────────┘
                                   │
                                  UART
                                   │
                                   ▼
              ┌────────────────────────────────────┐
              │               ECU 1                │
              │             LPC2129                │
              │                                    │
              │   RFID Authentication              │
              │   UART Communication               │
              │   GSM Notification                 │
              │   CAN Transmission                 │
              └─────────────────┬──────────────────┘
                                │
                                │ CAN BUS
                    ┌───────────┴───────────┐
                    │                       │
                    ▼                       ▼
          ┌───────────────────┐   ┌───────────────────┐
          │      ECU 2        │   │      ECU 3        │
          │     LPC2129       │   │     LPC2129       │
          │                   │   │                   │
          │ CAN Reception     │   │ CAN Reception     │
          │ PWM Control       │   │ 20×4 LCD          │
          │ Servo Control     │   │ LED + Buzzer       │
          └─────────┬─────────┘   └───────────────────┘
                    │
                    ▼
             ┌──────────────┐
             │ Servo Motor  │
             │ Gate Control │
             └──────────────┘
🔧 Hardware Components
Microcontroller
LPC2129 ARM7TDMI-S
ARM7 microcontroller
CAN controller
UART interface
PWM generation
GPIO
RFID Section
EM-18 RFID Reader
RFID Card/Tag
UART interface
Communication
CAN Bus
UART
GSM Module
Display and Alert
20×4 LCD
LED
Buzzer
Gate Control
Servo Motor
PWM Control
💻 Software and Tools
Embedded C
Keil µVision
ARM7 LPC2129 Development Environment
CAN Debugging Tools
⚙️ Working Principle
Step 1 — RFID Scanning

The RFID tag is placed near the EM-18 RFID reader.

The reader detects the RFID tag and obtains its identification value.

The RFID data is transferred to the LPC2129 through UART.

Step 2 — RFID Authentication

The LPC2129 receives the RFID value and compares it with the predefined authorized RFID.

Example:

Authorized RFID:
060067E061E0

If the received RFID matches:

VALID RFID

Otherwise:

INVALID RFID
Step 3 — CAN Communication

The authentication result is transmitted through the CAN bus.

The project uses:

CAN ID = 0x101

Authentication data:

0x01 → VALID RFID
0x02 → INVALID RFID
Step 4 — Gate Control

The gate-control ECU receives the CAN message.

For valid authentication:

Valid RFID
     ↓
CAN ID 0x101
ByteA = 0x01
     ↓
Servo rotates to 90°
     ↓
Gate Opens
     ↓
Wait for predefined time
     ↓
Servo returns to 0°
     ↓
Gate Closes

For invalid authentication:

Invalid RFID
     ↓
CAN ID 0x101
ByteA = 0x02
     ↓
Gate remains closed
Step 5 — LCD Display

The display ECU receives the CAN authentication result.

For valid RFID:

VALID RFID
ACCESS GRANTED

For invalid RFID:

INVALID RFID
ACCESS DENIED

The LCD can also display the project title:

BattleGuard: Advance
MILITARY ACCESS
RFID AUTHENTICATION
CAN COMMUNICATION

The complete project title can be scrolled across the first row of the 20×4 LCD.

Step 6 — Alert System

When unauthorized access is detected:

LED is activated.
Buzzer provides an alert.
GSM can send an SMS notification.

This provides both local and remote notification of unauthorized access.

🔄 Authentication Flow
             START
               │
               ▼
          Scan RFID Tag
               │
               ▼
       Read RFID through UART
               │
               ▼
       Compare with Stored ID
               │
          ┌────┴────┐
          │         │
        VALID     INVALID
          │         │
          ▼         ▼
      ByteA=01   ByteA=02
          │         │
          ▼         ▼
      CAN 0x101   CAN 0x101
          │         │
          ▼         ▼
      Gate Open  Gate Closed
          │
          ▼
      Gate Close
          │
          ▼
      Continue Scanning
📡 CAN Communication

CAN stands for Controller Area Network.

It is used for reliable communication between the different LPC2129 controller nodes.

CAN Message Format
Parameter	Value
CAN ID	0x101
DLC	1
Valid RFID	0x01
Invalid RFID	0x02

The authentication result is transferred using the first CAN data byte.

📺 20×4 LCD Display

The LCD uses four rows with 20 characters per row.

┌────────────────────┐
│ BattleGuard: Advance│
│ MILITARY ACCESS    │
│ RFID AUTHENTICATION│
│ CAN COMMUNICATION  │
└────────────────────┘

LCD row addresses:

Row 1 → 0x80
Row 2 → 0xC0
Row 3 → 0x94
Row 4 → 0xD4
🔌 Interfaces Used
Interface	Purpose
UART	RFID and GSM communication
CAN	Communication between LPC2129 nodes
PWM	Servo motor control
GPIO	LED, buzzer and control signals
LCD	System status display
✅ Advantages
Automated access authentication
Reduces manual verification
Fast RFID-based identification
Reliable CAN-based communication
Automatic gate operation
Real-time LCD status display
LED and buzzer alert system
GSM notification capability
Multi-node embedded architecture
Modular system design
Low-cost embedded implementation
Easy to expand with additional authentication methods
🚀 Applications

The system can be applied to:

Military restricted-area access control
Defence facility security
Industrial security systems
Secure vehicle entry systems
Research laboratories
Restricted office areas
Campus access control
Critical infrastructure security
Automated gate-control systems
🔮 Future Enhancements
Support multiple authorized RFID tags.
Store RFID IDs in EEPROM.
Add fingerprint authentication.
Add face recognition.
Add real-time clock for access logging.
Store entry and exit records.
Add wireless monitoring.
Develop a PC/mobile monitoring dashboard.
Add database-based authentication.
Add emergency override functionality.
📂 Project Structure
BattleGuard/
│
├── ECU1-RFID&GSM/
│   ├── RFID
│   ├── GSM
│   └── CAN
│
├── ECU2-Dashboard&LED/
│   ├── CAN
│   ├── LCD
│   ├── LED
│   └── Buzzer
│
└── ECU3-Servo_Motor/
    ├── CAN
    ├── PWM
    └── Servo Motor
🧠 Skills Demonstrated
Embedded C Programming
ARM7 LPC2129
RFID Interfacing
UART Communication
CAN Communication
PWM Programming
Servo Motor Control
LCD Interfacing
GSM Interfacing
GPIO Programming
Multi-node Embedded Systems
Hardware Interfacing
Embedded System Debugging
📌 Project Outcome

The project demonstrates an automated RFID-based access-control system using multiple LPC2129 controllers communicating through CAN.

The system integrates:

RFID Authentication
        +
UART Communication
        +
CAN Communication
        +
PWM Servo Control
        +
20×4 LCD
        +
LED & Buzzer
        +
GSM Notification
        =
BattleGuard

The project provides a practical demonstration of multi-node embedded system design, authentication, communication, and automated access control.

⭐ Project Highlights
Microcontroller: LPC2129 ARM7
Authentication: RFID
Communication: CAN
Serial Interface: UART
Gate Control: Servo + PWM
Display: 20×4 LCD
Alert: LED + Buzzer
Notification: GSM
Programming: Embedded C
Development Tool: Keil µVision
📜 License

This project is developed for educational and demonstration purposes.

give full like readme code

Yes — you want the entire README.md as one single Markdown code block, with no separate explanations, so you can copy it directly into GitHub.

# 🛡️ BattleGuard
## Advanced Military Access Control and Authentication System Using RFID and CAN Communication

---

## 📌 Project Overview

**BattleGuard** is an advanced multi-node embedded access control and authentication system designed for secure entry management in restricted and sensitive areas.

The system combines **RFID authentication, CAN communication, GSM notification, LCD monitoring, LED and buzzer alerts, and servo-based automatic gate control**.

The project is developed using **LPC2129 ARM7 microcontrollers**. Different controller nodes perform authentication, communication, display, alert, and gate-control functions.

This project demonstrates the practical implementation of **Embedded C programming, ARM7 microcontroller programming, UART, CAN, PWM, RFID, GSM, LCD, GPIO, and multi-node embedded system communication**.

---

## 📝 Abstract

Security and controlled access are essential requirements in military, defence, industrial, and other restricted environments. Manual authentication can be time-consuming and may increase the possibility of unauthorized access.

**BattleGuard** provides an automated RFID-based authentication and access-control solution using multiple LPC2129 microcontroller nodes.

An **EM-18 RFID reader** detects the RFID tag and sends its identification data to the LPC2129 through UART communication. The received RFID value is compared with a predefined authorized RFID ID.

If the RFID is valid, the authentication result is transmitted through the **CAN bus** to the other controller nodes. The gate-control node receives the valid authentication message and operates a servo motor using PWM to open the gate. After a predefined time, the gate automatically closes.

If an invalid RFID tag is detected, the gate remains closed. The display node shows the unauthorized access status on a **20×4 LCD**, while an LED and buzzer provide an alert indication. A GSM module can also be used to send an SMS notification for unauthorized access.

The project demonstrates a practical **distributed multi-node embedded security system using CAN communication**.

---

## 🎯 Objectives

- Implement RFID-based authentication.
- Read RFID data using UART communication.
- Compare the scanned RFID with an authorized RFID ID.
- Transfer authentication status using CAN communication.
- Control a servo motor using PWM.
- Implement automatic gate opening and closing.
- Display authentication status using a 20×4 LCD.
- Provide LED and buzzer alerts for unauthorized access.
- Send GSM notification for unauthorized access.
- Demonstrate multi-node communication using LPC2129.

---

# 🏗️ System Architecture

```text
                         ┌─────────────────────┐
                         │      RFID TAG       │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   EM-18 RFID        │
                         │      READER         │
                         └──────────┬──────────┘
                                    │
                                   UART
                                    │
                                    ▼
              ┌────────────────────────────────────┐
              │              ECU 1                 │
              │            LPC2129                │
              │                                    │
              │  RFID Authentication               │
              │  UART Communication                │
              │  GSM Notification                  │
              │  CAN Transmission                  │
              └─────────────────┬──────────────────┘
                                │
                                │ CAN BUS
                                │
                 ┌──────────────┴───────────────┐
                 │                              │
                 ▼                              ▼
       ┌─────────────────────┐       ┌─────────────────────┐
       │        ECU 2        │       │        ECU 3        │
       │       LPC2129       │       │       LPC2129       │
       │                     │       │                     │
       │ CAN Reception       │       │ CAN Reception       │
       │ PWM Control         │       │ 20×4 LCD            │
       │ Servo Control       │       │ LED + Buzzer         │
       └──────────┬──────────┘       └─────────────────────┘
                  │
                  ▼
          ┌─────────────────┐
          │   SERVO MOTOR   │
          │   GATE CONTROL   │
          └─────────────────┘
🔧 Hardware Components
Microcontroller
LPC2129 ARM7TDMI-S
ARM7 microcontroller
CAN controller
UART interface
PWM generation
GPIO
RFID Section
EM-18 RFID Reader
RFID Card / RFID Tag
UART interface
Communication
CAN Bus
UART
GSM Module
Display and Alert
20×4 LCD
LED
Buzzer
Gate Control
Servo Motor
PWM Control
Other Components
Power supply
Connecting wires
CAN transceiver/interface hardware
Development board
💻 Software and Development Tools
Embedded C
Keil µVision
ARM7 LPC2129 Development Environment
CAN Debugging Tools
⚙️ Working Principle
1️⃣ RFID Tag Detection

The RFID tag is placed near the EM-18 RFID reader.

The RFID reader generates an electromagnetic field. A passive RFID tag receives energy through electromagnetic induction and responds with its stored identification information.

The EM-18 reader receives and decodes the RFID information.

The RFID data is then transmitted serially to the LPC2129 through UART.

RFID Tag
   ↓
EM-18 Reader
   ↓
UART
   ↓
LPC2129
2️⃣ RFID Authentication

The LPC2129 receives the RFID identification value character by character.

The received RFID value is stored in a character buffer and compared with the predefined authorized RFID.

Example:

Authorized RFID:

060067E061E0

If the received RFID matches the authorized RFID:

VALID RFID

Otherwise:

INVALID RFID
3️⃣ CAN Communication

The authentication result is transmitted from the RFID node to the other controller nodes through the CAN bus.

CAN is used because it provides reliable communication between multiple microcontroller nodes.

The project uses:

CAN ID = 0x101

Authentication data:

0x01 → VALID RFID
0x02 → INVALID RFID
CAN Message Format
Parameter	Value
CAN ID	0x101
DLC	1
ByteA	0x01 → Valid
ByteA	0x02 → Invalid
🚪 4️⃣ Automatic Gate Control

The gate-control node receives the authentication result through CAN.

Valid RFID
Valid RFID
     ↓
CAN ID = 0x101
ByteA = 0x01
     ↓
CAN Reception
     ↓
Servo Motor
     ↓
Gate Opens
     ↓
Wait for predefined time
     ↓
Servo returns to 0°
     ↓
Gate Closes

The servo motor is controlled using PWM.

For example:

0°   → 1000 µs pulse
90°  → 1500 µs pulse
Invalid RFID
Invalid RFID
      ↓
CAN ID = 0x101
ByteA = 0x02
      ↓
CAN Reception
      ↓
Gate remains closed
📺 5️⃣ LCD Display

A 20×4 LCD is used to display system information and authentication status.

Startup Display
┌────────────────────┐
│ BattleGuard: Advance│
│ MILITARY ACCESS    │
│ RFID AUTHENTICATION│
│ CAN COMMUNICATION  │
└────────────────────┘

The complete project title can be smoothly scrolled across the first row.

Valid RFID
┌────────────────────┐
│ VALID RFID         │
│ ACCESS GRANTED     │
│                    │
│ GATE OPENING...    │
└────────────────────┘
Invalid RFID
┌────────────────────┐
│ INVALID RFID       │
│ ACCESS DENIED      │
│                    │
│ WARNING !!!        │
└────────────────────┘
🚨 6️⃣ Alert System

When an unauthorized RFID tag is detected:

INVALID RFID
     ↓
Gate remains closed
     ↓
LCD → ACCESS DENIED
     ↓
LED → ON
     ↓
Buzzer → ON
     ↓
GSM → SMS Alert

The GSM module can send a notification to a predefined mobile number.

🔄 Complete System Flow
                       START
                         │
                         ▼
                    Scan RFID
                         │
                         ▼
                  EM-18 Reader
                         │
                         ▼
                  Read RFID via UART
                         │
                         ▼
              Compare with Stored ID
                         │
                  ┌──────┴──────┐
                  │             │
                VALID         INVALID
                  │             │
                  ▼             ▼
              ByteA=01       ByteA=02
                  │             │
                  ▼             ▼
              CAN 0x101      CAN 0x101
                  │             │
          ┌───────┴───────┐     │
          │               │     │
          ▼               ▼     ▼
       Gate ECU       Display ECU
          │               │
          ▼               ▼
      Servo Open      LCD Display
          │           LED + Buzzer
          ▼               │
    Wait 5 Seconds        │
          │               │
          ▼               │
      Servo Close         │
          │               │
          └───────┬───────┘
                  │
                  ▼
             Continue Scan
📡 CAN Communication
Why CAN?

CAN (Controller Area Network) is a multi-node communication protocol commonly used in automotive and industrial embedded systems.

In this project, CAN provides communication between the different LPC2129 nodes.

CAN Communication
ECU 1
RFID Authentication
      │
      │ CAN BUS
      ▼
 ┌─────────────┐
 │ CAN ID 101  │
 └─────────────┘
      │
      ├──────────────► ECU 2
      │                Servo Gate Control
      │
      └──────────────► ECU 3
                       LCD + LED + Buzzer
🔌 Interfaces Used
Interface	Purpose
UART	RFID and GSM communication
CAN	Communication between LPC2129 nodes
PWM	Servo motor control
GPIO	LED, buzzer and control signals
LCD	Authentication and system status display
📺 LCD Pin Configuration

The 20×4 LCD uses the following LPC2129 connections:

LCD Signal	LPC2129 Pin
D0	P0.0
D1	P0.1
D2	P0.2
D3	P0.3
D4	P0.4
D5	P0.5
D6	P0.6
D7	P0.7
RS	P0.8
E	P0.9
LCD Row Addresses
Row 1 → 0x80
Row 2 → 0xC0
Row 3 → 0x94
Row 4 → 0xD4
🔌 UART Configuration

RFID communication is performed using UART.

RFID Reader → UART1 → LPC2129

Typical configuration used:

Baud Rate = 9600 bps
Data Bits = 8
Stop Bits = 1
Parity    = None
🎛️ PWM Servo Control

The servo motor is controlled using PWM.

PWM Frequency = 50 Hz
PWM Period    = 20 ms

Example:

Servo Position     Pulse Width

0°                 1000 µs
90°                1500 µs

The PWM signal is generated using PWM5 on P0.21 in the gate-control node.

🔐 Authentication Logic
if RFID == Authorized_ID
        |
        ├── YES
        │    |
        │    ├── CAN ByteA = 0x01
        │    ├── Gate Opens
        │    ├── LCD → VALID RFID
        │    └── ACCESS GRANTED
        │
        └── NO
             |
             ├── CAN ByteA = 0x02
             ├── Gate Remains Closed
             ├── LCD → INVALID RFID
             ├── LED + Buzzer
             └── GSM Alert
📂 Project Structure
BattleGuard/
│
├── ECU1-RFID&GSM/
│   │
│   ├── RFID
│   ├── GSM
│   ├── CAN
│   └── Embedded C Source Files
│
├── ECU2-Dashboard&LED/
│   │
│   ├── CAN
│   ├── LCD
│   ├── LED
│   ├── Buzzer
│   └── Embedded C Source Files
│
└── ECU3-Servo_Motor/
    │
    ├── CAN
    ├── PWM
    ├── Servo Motor
    └── Embedded C Source Files
🧩 Node Description
ECU 1 — RFID + GSM + CAN
Functions
RFID tag detection
RFID authentication
UART communication
CAN transmission
GSM notification
RFID
  ↓
UART
  ↓
LPC2129
  ↓
Authentication
  ↓
CAN
  ↓
Other ECUs
ECU 2 — Dashboard + LED + Buzzer
Functions
CAN reception
Authentication status display
LED indication
Buzzer alert
CAN
 ↓
LPC2129
 ↓
LCD
LED
Buzzer
ECU 3 — Servo Motor Gate Control
Functions
CAN reception
Authentication verification
PWM generation
Servo motor control
Automatic gate operation
CAN
 ↓
LPC2129
 ↓
PWM
 ↓
Servo Motor
 ↓
Gate
🛠️ Technologies Used
Embedded C
ARM7 LPC2129
RFID
EM-18 RFID Reader
CAN
UART
GSM
PWM
20×4 LCD
Servo Motor
GPIO
Keil µVision
🧠 Skills Demonstrated
Embedded C Programming
ARM7 Microcontroller Programming
UART Communication
CAN Communication
RFID Interfacing
GSM Interfacing
PWM Programming
Servo Motor Control
LCD Interfacing
GPIO Programming
Multi-node Embedded System Design
Hardware Interfacing
Embedded System Debugging
Hardware and Software Integration
✅ Advantages
Automated access authentication
Reduces manual verification
Fast RFID-based identification
Reliable CAN-based communication
Automatic gate operation
Real-time LCD status monitoring
LED and buzzer warning system
GSM notification capability
Multi-node embedded architecture
Modular system design
Easy to expand
Suitable for restricted-area access management
Demonstrates real-time embedded communication
🚀 Applications

The system can be used or adapted for:

Military restricted-area access control
Defence facility security
Secure vehicle entry systems
Industrial facility access control
Research laboratories
Restricted office areas
Campus access control
Critical infrastructure security
Automated gate-control systems
Secure parking access systems
🔮 Future Enhancements
Support multiple authorized RFID tags.
Store RFID IDs in EEPROM.
Add fingerprint authentication.
Add face recognition.
Add real-time clock (RTC).
Maintain entry and exit logs.
Add database-based authentication.
Add wireless monitoring.
Develop a PC/mobile monitoring dashboard.
Add cloud-based access monitoring.
Add event logging for authorized and unauthorized attempts.
Add additional authentication layers for improved security.
📊 System Features
Feature	Implementation
Authentication	RFID
RFID Reader	EM-18
Microcontroller	LPC2129 ARM7
Communication	CAN
Serial Communication	UART
Gate Control	Servo Motor
Motor Control	PWM
Display	20×4 LCD
Alert	LED + Buzzer
Remote Notification	GSM
Programming	Embedded C
IDE	Keil µVision
📌 Project Outcome

The BattleGuard project successfully demonstrates an automated RFID-based access-control system using multiple LPC2129 microcontrollers communicating through CAN.

The system integrates:

RFID Authentication
        +
UART Communication
        +
CAN Multi-Node Communication
        +
PWM Servo Control
        +
20×4 LCD Display
        +
LED & Buzzer Alert
        +
GSM Notification
        =
       🛡️
   BATTLEGUARD

The project provides practical experience in embedded system design, microcontroller programming, hardware interfacing, communication protocols, authentication logic, and multi-node control systems.

⭐ Project Highlights
🔐 RFID-based authentication
📡 CAN-based multi-node communication
📟 LPC2129 ARM7 microcontroller
🚪 Automatic servo-controlled gate
📺 20×4 LCD monitoring
🚨 LED and buzzer alert
📱 GSM notification
⚡ PWM-based servo control
🔌 UART communication
💻 Embedded C programming
🛠️ Keil µVision development
👩‍💻 Author

Poomalar R

B.E. Electrical and Electronics Engineering

GitHub

https://github.com/poomalar258-code

📜 License

This project is developed for educational and demonstration purposes.
