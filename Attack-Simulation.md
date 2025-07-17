# 🛡️ CAN Bus Attack Simulations

This module demonstrates various **cyberattacks on the CAN bus** system implemented on **Infineon AURIX™ TC397** boards. Each attack showcases vulnerabilities and how our system filters or reacts to malicious messages.

---

## 🚀 Attack Setup

- **Tools Used**:
  - BusMaster (Simulation & injection)
  - Vector CAN Interface
  - AURIX™ TC397 Transmitter & Receiver boards
  - LED D107 (TX) and D108 (RX) indicators

---

## ⚔️ Attack #1 – Denial of Service (DoS)

**📝 Description:**  
Floods the CAN bus with high-priority messages (`ID = 0x000`) to block legitimate traffic.

**📷 Observations:**
- Receiver stops processing valid messages (`ID = 0x77`)
- LED D108 (RX) doesn't blink
- BusMaster shows continuous ID `0x000` flooding

**✅ Outcome:**  
Proves CAN arbitration vulnerability – higher priority IDs dominate.

---

## 🧪 Attack #2 – Fuzzing

**📝 Description:**  
Sends randomized/malformed payloads under a valid CAN ID (`0x77`) to confuse ECUs.

**📷 Observations:**
- Receiver accepts packets but fails payload checks
- LED D108 may blink, but decoded data is garbage
- No error flags due to valid ID

**✅ Outcome:**  
Bypasses ID filtering, highlighting need for payload-level validation.

---

## 🕵️ Attack #3 – Spoofing

**📝 Description:**  
Sends forged payloads using the **same valid CAN ID** as the trusted transmitter (`ID = 0x77`).

**📷 Observations:**
- Receiver cannot distinguish between real and spoofed messages
- LED D108 blinks even for malicious data
- BusMaster log shows similar IDs with different payloads

**✅ Outcome:**  
Shows that **ID-based filtering is insufficient** – authentication mechanisms (like SecOC) are needed.

---

## 📁 Files Included (Optional)

