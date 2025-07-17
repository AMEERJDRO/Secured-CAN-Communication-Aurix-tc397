# 📊 Results and Analysis – Secure CAN Communication Project

This document presents the **experimental results and findings** from our project:  
🔐 _"Secured CAN Communication and Attack Simulation on Infineon AURIX TC397"_

---

## ✅ Summary of Experiments

| Test Case                                   | Expected Outcome                                 | Result        | LED Status  |
|--------------------------------------------|--------------------------------------------------|---------------|-------------|
| LED GPIO Test                               | LED D107 blinks at 1 Hz                          | ✅ Success     | Blinking    |
| Loopback CAN (Node 0 → Node 1 same board)   | TX & RX LEDs toggle on valid message             | ✅ Success     | D107 & D108 |
| Inter-board CAN TX/RX (2 TC397 boards)      | LED D108 blinks on valid payload `0x77`          | ✅ Success     | Blinking    |
| Message Filtering (valid ID = 0x77)         | Messages with wrong ID rejected                  | ✅ Success     | No blink    |
| DoS Attack (ID = 0x000 flood)               | RX blocks; LED D108 stops blinking               | ✅ Success     | OFF         |
| Fuzzing Attack (random payloads, ID = 0x77) | RX accepts ID, fails payload validation          | ⚠️ Partial    | D108 blinks |
| Spoofing Attack (fake payload, ID = 0x77)   | RX can't detect spoofed message without SecOC    | ❌ Fail        | D108 blinks |




## 🧪 Observations

- **LEDs D107 (TX) and D108 (RX)** provided real-time verification of message flow.
- **BusMaster** logs confirmed message integrity and attack injections.
- **DoS** was the most effective attack — it successfully blocked all normal frames.
- **Spoofing** bypassed filtering due to use of valid CAN IDs.

---

## 🔬 Limitations

- Message filtering is **based on CAN ID** only; no payload or sender verification.
- No cryptographic methods used — leaving the system open to spoofing or replay attacks.
- Fuzzing detection requires deeper payload inspection or checksum validation.

---

## 🧠 Key Takeaways

- CAN is efficient, but **insecure by design**.
- Interrupt-based filtering provides basic protection.
- Further protection (AUTOSAR SecOC, MAC checks) is **strongly recommended** for production-grade automotive systems.

---

## 📎 Files Included 

- [SPOOFING.pdf](https://github.com/user-attachments/files/21294053/SPOOFING.pdf) 
- [FUZZING.pdf](https://github.com/user-attachments/files/21294051/FUZZING.pdf)
