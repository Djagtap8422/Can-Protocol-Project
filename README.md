# CAN_PROTOCOL_PROJECT
Alright — here’s a **different format** for your README.
This one uses a **problem–solution–implementation** approach with a **story-like flow**,
so it feels less like a parts list and more like a professional project report summary.

---

# 🚘 VECTOR\_MAJOR\_PROJECT

## Real-Time Vehicle Status Monitoring System – CAN Protocol (LPC2129)

## 1️⃣ *Project Overview*

Modern vehicles rely on multiple Electronic Control Units (ECUs) communicating seamlessly to monitor and control various subsystems.
This project replicates such a **real-time, multi-node communication network** using **CAN protocol** on the **LPC2129 ARM7 microcontroller**.
Three specialized nodes exchange data to simulate a vehicle’s dashboard and sensor network.

---

### 2️⃣ *The Challenge*

* In a real vehicle, the fuel sensor, indicator switches, and dashboard display are physically separate.
* These components must communicate without wiring each one directly to every other — a complex and error-prone approach.
* The system must be **robust**, **fault-tolerant**, and **scalable** for future expansion.

---

## 3️⃣ *Our Solution*

We implemented a **Controller Area Network (CAN)** based distributed system with three dedicated embedded nodes:

1. Main Node – Acts as the central dashboard, displaying all received information.
2. Indicator Node – Detects left/right turn signals via external switches.
3. Fuel Node – Reads fuel level through ADC from an analog sensor.

---

## 4️⃣ **System Architecture**

```
[Indicator Node] ---\
                      >--- [CAN Bus] --- [Main Node with LCD]
[Fuel Node] ---------/
```

* **CAN Bus Speed:** Up to 1 Mbps
* **Message IDs:**

* `0x100` – Indicator Node data
* `0x200` – Fuel Node data
* Data Frame:* 8-byte payload with sensor/control values

---

## 5️⃣ *Node Functionality Details*

## 🟢 Main Node – Dashboard Controller

* Receives CAN messages from both other nodes.
* Displays direction (LEFT/RIGHT/OFF) and fuel percentage.
* Provides clear, human-readable output on a **16×2 LCD**.

#### 🟡 Indicator Node – Signal Controller

* Uses interrupt-based detection of switch presses.
* Sends **turn signal status** via CAN frames.
* Ensures minimal latency for immediate status update.

## 🔵 Fuel Node – Sensor Interface

* Uses ADC to read analog voltage from the fuel sensor.
* Converts reading to percentage and transmits via CAN.
* Encodes value in 8-byte CAN message payload.

---

## 6️⃣ *Hardware Components*

| Hardware         | Function                     |
| ---------------- | ---------------------------- |
| LPC2129          | ARM7 MCU, controls all nodes |
| MCP2551          | CAN transceiver IC           |
| 16×2 LCD         | Display for Main Node        |
| Fuel Sensor      | Analog fuel level input      |
| Switches & LEDs  | Indicator control simulation |
| MMA7660          | Optional accelerometer       |
| Regulated 5V PSU | Power source                 |

---

### 7️⃣ **Development Tools**

* Keil µVision – Embedded C coding & debugging
* Flash Magic – HEX file flashing to LPC2129
* Proteus – Circuit simulation *(optional)*
* GitHub – Version control & project tracking

---

### 8️⃣ **Folder Structure**

```
VECTOR_MAJOR_PROJECT/
  ├── MAIN_NODE/
  │   ├── main_node.c
  │   ├── lcd.c / lcd.h
  │   ├── can.c / can.h
  │   ├── delay.c / delay.h
  │   └── types.h
  │
  ├── INDICATOR_NODE/
  │   ├── indicator_node.c
  │   ├── can.c / can.h
  │   ├── delay.c / delay.h
  │   └── types.h
  │
  ├── FUEL_NODE/
      ├── fuel_node.c
      ├── adc.c / adc.h
      ├── can.c / can.h
      ├── delay.c / delay.h
      └── types.h
```

---

### 9️⃣ **Key Advantages**

* Scalable: Easy to add new nodes (temperature, RPM, etc.) without redesigning the wiring.
* Reliable: CAN’s error detection ensures accurate communication.
* Modular: Each node is independent, reducing complexity and improving maintenance.

---
