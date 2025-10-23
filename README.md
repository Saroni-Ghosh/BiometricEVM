
#  Biometric-Based Electronic Voting Machine (EVM) using Arduino

##  Project Overview
This project implements a **biometric-based electronic voting system** that enhances election transparency and voter authentication using **fingerprint verification**.  
It ensures **secure, one-person-one-vote** principles by integrating **fingerprint sensors, an LCD display, LEDs, a buzzer, and EEPROM** with an **Arduino Uno**.

Voters and officers must authenticate their fingerprints before a vote can be cast, ensuring both authorization and accountability.

---

##  Key Features
-  **Biometric Authentication** – Fingerprint verification for both voter and officer.  
-  **Electronic Voting** – Cast votes for three parties using dedicated buttons.  
-  **EEPROM Integration** – Stores vote counts even after power is turned off.  
-  **LCD Display (I2C)** – Displays user instructions, verification results, and final vote tally.  
-  **Buzzer and LED Alerts** – Provide audio-visual feedback for each action.  
-  **Delete / Result Button** – Short press to show results; long press to clear vote data.  
-  **Two-Factor Security** – Officer + Voter fingerprint verification before voting.

---

##  Components Used
| Component | Description | Arduino Pins |
|------------|--------------|---------------|
| **Arduino Uno** | Main microcontroller | — |
| **Fingerprint Sensor 1 (Voter)** | Fingerprint module (R305 or similar) | TX → D10, RX → D11 |
| **Fingerprint Sensor 2 (Officer)** | Fingerprint module | TX → D8, RX → D9 |
| **LCD 16x2 (I2C)** | Displays instructions and results | SDA → A4, SCL → A5 |
| **Buzzer** | Audio alert | D3 |
| **Party Buttons** | Voting buttons (3) | D4, D5, D6 |
| **Enroll Button** | Register new fingerprint | A0 |
| **Match Button** | Authenticate voter/officer | A1 |
| **UP/DOWN Buttons** | Navigate fingerprint IDs | A2, A3 |
| **Result/Delete Button** | Short = Show Result, Long = Clear Data | D6 |
| **LEDs (Green/Red)** | Match/Fail Indicators for voter and officer | D6 (voter), D7 (officer) |
| **Power Switch** | ON/OFF toggle from 9V battery | VIN and GND |

---

##  Circuit Summary
- **Dual Fingerprint Sensors**: Separate serial connections for voter and officer.
- **LCD I2C Display**: Uses SDA/SCL pins (A4, A5) for communication.
- **EEPROM**: Stores vote counts persistently.
- **LEDs & Buzzer**: Provide clear feedback for system states.
- **Switch & Battery**: Allows standalone portable operation.

---

##  Software Setup

### 1. **Required Libraries**
Install these from **Arduino IDE → Sketch → Include Library → Manage Libraries**:
- `Adafruit Fingerprint Sensor Library`
- `LiquidCrystal_I2C`
- `EEPROM`

### 2. **Board & Port Setup**
- **Board:** Arduino Uno  
- **Port:** COMx (detected automatically after USB connection)  
- **Baud Rate:** 9600  

### 3. **Upload Steps**
1. Open the `.ino` file in Arduino IDE  
2. Verify (✅) and Upload (→)  
3. Open **Serial Monitor** (9600 baud) for debugging or fingerprint enrollment

---

##  System Workflow

### 1. **Enrollment Phase**
- Press **Enroll (A0)** → Place and re-place the finger.  
- LCD: `Enroll Success` → Fingerprint ID stored.

### 2. **Authentication Phase**
- Officer verifies first → “Officer Verified”  
- Voter verifies → “Voter Verified”  
- Then, LCD prompts: `Cast Your Vote`

### 3. **Voting Phase**
- Press one of:
  - `D4` → Party 1  
  - `D5` → Party 2  
  - `D6` → Party 3  
- LCD: `Vote Casted` → Buzzer beeps → Vote stored in EEPROM.

### 4. **Result / Reset Phase**
- Short press **D6** → Display results  
- Long press **D6 (>2s)** → Clear all votes from EEPROM

---

## 🔍 Troubleshooting Guide

| Issue | Possible Cause | Solution |
|--------|----------------|----------|
| LCD blank | Wrong I2C address | Run I2C scanner; update address to 0x27 or 0x3F |
| Finger not detected | TX/RX swapped | Swap sensor TX/RX wires |
| EEPROM not saving votes | Incorrect write logic | Use `EEPROM.write()` or `EEPROM.update()` |
| Loose wires | Breadboard issues | Use shorter wires or solder connections |

---

##  Security & Ethical Considerations
- Fingerprints are **stored locally** on sensors (not in cloud).  
- Each fingerprint is **matched by unique ID**, preventing impersonation.  
- **Officer + Voter** dual verification prevents vote duplication.  
- Prototype only – not certified for government election use.

---

##  Future Improvements
- Add **GSM or Wi-Fi module** for remote result transmission  
- Use **encrypted fingerprint storage**  
- Implement **face recognition** for multimodal authentication  
- Design a **custom PCB** for compact and durable deployment  

---

##  Project Demo
##  Circuit Image  
[![View Circuit Image](https://drive.google.com/uc?export=view&id=15nSHceNXgmi-vk92FfQEN-vr0WPQUHT_)](https://drive.google.com/drive/folders/15nSHceNXgmi-vk92FfQEN-vr0WPQUHT_)

##  Demo Video  
 [Click here to watch the demo video](https://drive.google.com/drive/folders/15nSHceNXgmi-vk92FfQEN-vr0WPQUHT_)



---

##  References
- [Adafruit Fingerprint Sensor Library Docs](https://github.com/adafruit/Adafruit-Fingerprint-Sensor-Library)  
- [Arduino EEPROM Reference](https://www.arduino.cc/en/Reference/EEPROM)  
- [LiquidCrystal_I2C Documentation](https://github.com/johnrickman/LiquidCrystal_I2C)  

---

###  Final Note
This project demonstrates how **biometric security can enhance electronic voting** by reducing fraud and ensuring trust.  
A reliable and scalable version could transform the future of secure, paperless elections.

---

