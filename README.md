<h1 align="center">🔐 Secured CAN Communication & Attack Simulation</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Project-Minor--VI--Sem-blue" />
  <img src="https://img.shields.io/badge/Board-AURIX™%20TC397-orange" />
  <img src="https://img.shields.io/badge/BusMaster-Attack%20Simulation-red" />
</p>

---

## 📘 Abstract

Modern vehicles use CAN for critical communication between ECUs. However, CAN lacks security, making it vulnerable to spoofing, fuzzing, and DoS attacks. In this project, we implemented secured CAN communication between two **Infineon AURIX™ TC397** boards, and simulated real-world attacks using **BusMaster**.

🔒 Features:
- Interrupt-driven CAN communication
- CAN ID filtering (0x77)
- LED status indication
- Attack simulation using BusMaster (DoS, Spoofing, Fuzzing)
- Real-time monitoring with Vector CAN interface

---

## 🎯 Project Objectives

- Understand AUTOSAR architecture and CAN protocol.
- Implement secure inter-ECU communication using AURIX TC397.
- Simulate and analyze spoofing, fuzzing, and DoS attacks.
- Lay the foundation for Secure Onboard Communication (SecOC).

---

## 🛠️ System Design

### CAN Frame Format Overview

The CAN protocol uses a structured data frame for reliable message transfer between ECUs:
<img width="1332" height="471" alt="image" src="https://github.com/user-attachments/assets/f160d005-8cd5-4330-ba28-4ac99fc18d73" />


- **SOF**: Start of Frame  
- **ID**: Identifier (message priority)  
- **DLC**: Data Length Code (0-8 bytes)  
- **Data**: Actual payload  
- **CRC**: Error checking  
- **ACK**: Acknowledgment  
- **EOF**: End of Frame

> The CAN ID and Data field were crucial in our filtering and spoofing simulations.


### Hardware Setup
<img width="1188" height="611" alt="image" src="https://github.com/user-attachments/assets/bd48217b-f81c-4e9c-b043-8a476f81824b" />



- 2 × AURIX TC397 Boards
- 120Ω CAN termination
- LEDs for TX/RX status
- Vector CAN cable + BusMaster

### Communication Modes

| Mode           | Description                                  |
|----------------|----------------------------------------------|
| Loopback       | Internal CAN node-to-node test               |
| Inter-board TX | Transmitter sends ID: 0x77 → LED D107 blinks |
| Inter-board RX | Receiver filters & blinks LED D108           |

---

## 🧪 Attack Simulations

| Attack Type     | ID Used   | Effect                                               |
|------------------|-----------|------------------------------------------------------|
| DoS Attack       | `0x000`   | Floods the bus to block legitimate IDs              |
| Fuzzing Attack   | `0x077`   | Sends malformed/random payloads                     |
| Spoofing Attack  | `0x077`   | Sends forged data mimicking a trusted ECU           |

> 💡 Real-time analysis using BusMaster & LED status indicators

---

## 📂 Project Structure

```bash
/code
├── transmitter       # Sends ID 0x77 payloads
├── receiver          # Filters & receives ID 0x77
├── loopback          # Node 0 → Node 1 on same board
└── attacks           # Spoofing / Fuzzing / DoS demos

/docs
└── MINOR_REPORT_FINAL.pdf

/images
└── setup_diagram.png
