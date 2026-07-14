# Lab 4: Familiarization with Sensors, Actuators, and Embedded Systems

## Title
**Familiarization with Sensors, Actuators, and Embedded Systems**

## Objectives
- Understand the basic architecture of embedded systems used in IoT.  
- Become familiar with commonly used sensors and actuators.  
- Identify the features, functions, and pin configuration of the Raspberry Pi.  
- Identify the features, functions, and pin configuration of the ESP32.  
- Identify the features, functions, and pin configuration of the ESP8266.  
- Identify the features, functions, and pin configuration of the Arduino Uno.  

---

## Introduction
An embedded system is a combination of hardware and software designed to perform a specific, dedicated function within a larger system. In IoT, embedded systems form the "brain" of every smart device: a microcontroller or single-board computer receives input from sensors, processes the information according to programmed logic, and produces output through actuators or network communication.

 "Basic Embedded IoT Data Flow: Sensor (Input) → Microcontroller/Microprocessor (Processing) → Actuator / Network (Output)"  
 "An embedded system combines a processor (microcontroller or microprocessor), memory, input/output interfaces, and firmware to carry out a defined task."

---

## Background Theory

### Embedded Systems
Embedded systems combine a processor (microcontroller or microprocessor), memory, I/O interfaces, and firmware to perform dedicated tasks. Key characteristics include:
- **Real-time operation**: Many embedded systems must respond within strict timing constraints.  
- **Dedicated functionality**: Built for a specific purpose rather than general computing.  
- **Resource constraints**: Limited processing power, memory, and power supply.  
- **Reliability**: Expected to run continuously, often unattended.

# Image
<img width="481" height="415" alt="embedded system" src="https://github.com/user-attachments/assets/7c963d55-8d1e-4392-85a9-0f21aaaf7493" />


Embedded IoT devices typically fall into two categories:
- **Microcontroller-based boards** (Arduino Uno, ESP32, ESP8266): run a single program in a loop and directly control GPIO pins.  
- **Microprocessor-based boards** (Raspberry Pi): run a full OS (e.g., Raspberry Pi OS) and can multitask for heavier computation.

### Microcontrollers and Microprocessors for IoT

#### A. Raspberry Pi (Raspberry Pi 4 Model B)
**Use case:** Edge computing, local dashboards, camera-based systems.  
**Key specifications:**
- Processor: Broadcom BCM2711, Quad-core Cortex-A72 @ 1.5 GHz  
- RAM: 2 GB / 4 GB / 8 GB LPDDR4  
- Connectivity: Dual-band Wi‑Fi, Bluetooth 5.0, Gigabit Ethernet  
- USB: 2× USB 3.0, 2× USB 2.0  
- Display: 2× Micro-HDMI (dual 4K)  
- GPIO: 40-pin header (26 general-purpose usable GPIO)  
- Power: USB Type-C  
**Notes:** All GPIO pins operate at **3.3V logic**; connecting 5V directly can damage the board.

  # Image
  <img width="2560" height="1358" alt="Raspberry-Pi-4-Pinout-" src="https://github.com/user-attachments/assets/b2aa627a-1796-4eab-baad-a762816f1e63" />


#### B. ESP32
**Use case:** Wireless sensor nodes with higher processing and I/O needs.  
**Key specifications:**
- Processor: Dual-core Xtensa LX6 @ up to 240 MHz  
- Connectivity: Wi‑Fi + Bluetooth (Classic + BLE)  
- GPIO: Up to ~34 usable GPIO pins  
- ADC: 2× 12-bit ADC (up to 18 channels)  
- DAC: 2× 8-bit DAC (GPIO25, GPIO26)  
- PWM: 16 LEDC channels  
- Operating voltage: 3.3V  
**Notes:** Many peripheral functions can be reassigned to different GPIOs via pin multiplexing.

  # Image
  <img width="1366" height="780" alt="ESP32-DevKit-V1-Pinout-Diagram" src="https://github.com/user-attachments/assets/9975f2d1-e922-4ddd-ac61-c5bbb66c355f" />


#### C. ESP8266 (NodeMCU / ESP-12E)
**Use case:** Simple, low-cost Wi‑Fi sensor nodes.  
**Key specifications:**
- Processor: Tensilica L106 32-bit RISC @ 80–160 MHz  
- Connectivity: Wi‑Fi only  
- RAM/Flash: ~128 KB RAM, 4 MB Flash (typical module)  
- GPIO: ~11 recommended usable pins  
- Analog input: 1 pin (A0, 0–3.3V)  
- Operating voltage: 3.3V  
**Notes:** Silkscreen labels (D0–D8) differ from raw GPIO numbers; some pins are tied to flash and must not be used.

  # Image
  <img width="817" height="542" alt="ESP8266-NodeMCU-kit-12-E-pinout-gpio-pin" src="https://github.com/user-attachments/assets/cb53c0e4-37be-4df8-bb7e-d84a3248919f" />


#### D. Arduino Uno (R3)
**Use case:** Beginner-friendly microcontroller for simple sensor/actuator interfacing.  
**Key specifications:**
- Microcontroller: ATmega328P @ 16 MHz  
- Digital I/O: 14 pins (6 PWM-capable)  
- Analog inputs: 6 (A0–A5), 10-bit ADC  
- Flash / SRAM / EEPROM: 32 KB / 2 KB / 1 KB  
- Operating voltage: 5V (I/O logic 5V)  
**Notes:** Requires level shifting when interfacing with 3.3V devices.

  # Image
  <img width="1023" height="724" alt="Arduino uno pinout" src="https://github.com/user-attachments/assets/3cecdb31-c732-4887-8745-7e8936d37e71" />


### Comparison Summary
| Parameter | Raspberry Pi 4 | ESP32 | ESP8266 | Arduino Uno |
|-----------|----------------|-------|---------|-------------|
| Type | Microprocessor (runs OS) | Microcontroller (SoC) | Microcontroller (SoC) | Microcontroller |
| Built-in Wi‑Fi | Yes | Yes | Yes | No |
| Built-in Bluetooth | Yes | Yes | No | No |
| Logic Voltage | 3.3V | 3.3V | 3.3V | 5V |
| Usable GPIO | ~26 | ~34 | ~11 | 14 digital + 6 analog |
| Typical Use | Heavy processing, hosting servers | Wireless sensor nodes | Simple wireless nodes | Simple sensor/actuator interfacing |

---

## Sensors (Common IoT Sensors)
# **DHT11 / DHT22**
- Digital temperature and humidity sensors using a single-wire timing protocol.


<img width="480" height="360" alt="dht11-dht22-" src="https://github.com/user-attachments/assets/7a590740-972c-44cf-927b-906d1533d263" />



# **Light Sensor (LDR)**
- Photoresistor used in a voltage divider and read via analog input.

<img width="500" height="400" alt="Light Sensor(LDR)" src="https://github.com/user-attachments/assets/b653dcbe-7fe1-45f5-8f47-ff89b8a1176d" />


# **Soil Moisture Sensor**
- Two-probe resistance-based sensor producing analog voltage proportional to moisture.

<img width="678" height="452" alt="Soil moisture sensor" src="https://github.com/user-attachments/assets/6239ddfd-692b-4c1c-9e5c-2d7fc54bae61" />


# **Ultrasonic Distance Sensor (HC-SR04)**
- Measures distance by timing ultrasonic echo return.

<img width="447" height="447" alt="Ultrasonic Distance Sensor" src="https://github.com/user-attachments/assets/b1c85638-7f14-4418-aa5a-f9b68fc51c55" />



# **Gas Sensor (MQ series)**
- Detects gas concentrations by resistance changes when exposed to target gases.
<img width="617" height="463" alt="gas sensor" src="https://github.com/user-attachments/assets/36595448-1038-4124-a315-261d89504859" />

---

## Actuators (Common IoT Actuators)
# **LEDs** 
- Simple indicators; can be dimmed with PWM.  
<img width="447" height="447" alt="leds" src="https://github.com/user-attachments/assets/d650101f-0e41-486c-a38a-9dfaf8b7ee9c" />

#  **Buzzers**
- Active or passive for audible alerts. 
<img width="700" height="438" alt="Buzzers" src="https://github.com/user-attachments/assets/9dbf7edd-612d-404b-9b69-c84137463df9" />

# **Servo Motors**
- Position control via PWM for precise angular movement.  
<img width="1200" height="900" alt="Servo Motor" src="https://github.com/user-attachments/assets/acbd6549-7d20-4225-bb49-b18594469c77" />

# **DC Motors**
- Continuous rotation; require motor drivers (e.g., L298N).  
<img width="800" height="800" alt="dc motors" src="https://github.com/user-attachments/assets/df0af567-cc96-4ee8-bd47-cd912f03c375" />

# **Relay Modules**
- Electrically isolate and switch high-voltage/high-current loads.
<img width="1200" height="1200" alt="Relay Modules" src="https://github.com/user-attachments/assets/3a7c22ed-a76c-4dcc-9984-e910fe7fb491" />


---

## Procedure
- Studied embedded system architecture relevant to IoT.  
- Examined datasheets and pinout diagrams for Raspberry Pi, ESP32, ESP8266, and Arduino Uno.  
- Compared boards by processing power, connectivity, GPIO count, and logic voltage.  
- Identified common IoT sensors and actuators and their interfacing requirements.  
- Prepared summarized notes and comparison tables for hardware selection.  
- Researched real-world IoT projects to understand practical applications and design lessons.

---

## Research Work: 10 IoT Projects (Revised)
| # | Project Title | Brief Description | Reflection | Resource Link |
|---|---------------|-------------------|------------|---------------|
| 1 | Smart Greenhouse Controller | Uses Raspberry Pi + DHT22, soil moisture sensors, and relay-controlled irrigation and ventilation to maintain optimal plant conditions. | Demonstrates closed-loop control and scheduling; highlights sensor fusion and actuator safety. | [Smart Greenhouse Controller ](https://www.scribd.com/document/499625628/SmartGreenhouseSystem)|
| 2 | Wearable Health Monitor | Uses ESP32 with pulse and accelerometer sensors to track heart rate and activity, sending summaries to a mobile app. | Shows low-power design and secure BLE data transfer; useful for personal health telemetry. | [Wearable Health Monitor](https://www.scribd.com/document/814737986/CBM370-Wearable-Devices) |
| 3 | LoRa Asset Tracker | Combines GPS module with an ESP32/LoRa node to report location of assets over long range to a LoRaWAN gateway. | Illustrates trade-offs between power, range, and update frequency for remote tracking. |[ LoRa Asset Tracker ](https://www.scribd.com/document/741047059/LoRa-IoT-Asset-Tracking-System)|
| 4 | Smart Street Lighting | Uses ESP8266 nodes with LDRs and motion sensors to dim or brighten street lights and report energy usage to a central server. | Highlights energy savings and distributed coordination; emphasizes robust OTA update strategies. | [Smart Street Lighting](https://www.scribd.com/document/426116976/Smart-Street-Lighting) |
| 5 | Predictive Motor Maintenance | Raspberry Pi collects vibration and temperature data from industrial motors; edge ML model predicts bearing failure. | Demonstrates edge analytics and the value of early-warning systems to reduce downtime. |[ Predictive Motor Maintenance](https://www.scribd.com/document/418132849/Electric-Motor-PdM) |
| 6 | Air Quality Monitoring Network | Network of low-cost ESP32 sensor nodes measuring PM2.5, CO₂, and VOCs, aggregated to a cloud dashboard for city-scale monitoring. | Shows calibration challenges and the importance of data validation for environmental sensing. | [Air Quality Monitoring Network](https://www.scribd.com/presentation/415069448/Air-Quality-Monitoring) |
| 7 | Smart Irrigation with Weather Integration | ESP32-based soil moisture sensing combined with weather API data to optimize irrigation schedules and conserve water. | Combines local sensing with cloud data; demonstrates API integration and decision logic. | [Smart Irrigation with Weather Integration](https://www.scribd.com/document/718649975/Abstract-Smart-Irrigation-System) |
| 8 | Wildlife Camera Trap with Edge AI | Raspberry Pi + camera + lightweight object detection model to capture and classify wildlife, uploading images when target species detected. | Useful for conservation; highlights power management and model optimization for edge devices. | [Wildlife Camera Trap with Edge AI](https://www.scribd.com/presentation/861994737/An-Introduction-to-Camera-Trapping-for-Wildlife-Surveys) |
| 9 | Smart Refrigerator Inventory | ESP32 + weight sensors and RFID tags to track items inside a refrigerator and notify users when supplies run low. | Demonstrates multi-sensor fusion and user-facing notifications; useful for inventory automation. | [Smart Refrigerator Inventory](https://www.scribd.com/presentation/522145308/Smart-Fridge) |
| 10 | Industrial Vibration Monitoring | ESP32 or Arduino with accelerometer modules streaming vibration spectra to a server for FFT analysis and anomaly detection. | Reinforces signal processing basics and the need for reliable sampling and time synchronization. | [Industrial Vibration Monitoring](https://www.scribd.com/document/226670708/Vibration) |

---

## Output
- Clear understanding of embedded system architecture in the context of IoT.  
- Familiarity with features, specifications, and pin configurations of Raspberry Pi, ESP32, ESP8266, and Arduino Uno.  
- Ability to select the right board for a given IoT task based on connectivity, processing power, and GPIO requirements.  
- Understanding of common IoT sensors and actuators and how they interface with microcontrollers.  
- Exposure to 10 real-world IoT projects and the design lessons they offer.

---

## Conclusion
- This laboratory experiment established a comprehensive foundation in the hardware architecture driving modern IoT and embedded systems. A comparative analysis of popular boards—namely the Raspberry Pi, ESP32, ESP8266, and Arduino Uno—demonstrated that optimal hardware selection is inherently driven by application-specific demands, requiring a careful balance of processing capabilities, native wireless support, GPIO pin count, and operating voltages. Furthermore, the examination of standard peripheral devices, including various sensors (e.g., DHT11/22, LDR, ultrasonic, gas) and actuators (e.g., relays, servos, buzzers), successfully illustrated the fundamental input-output mechanisms necessary for interacting with the physical world. By bridging these theoretical concepts with the analysis of ten practical use cases, several critical applied system design principles were reinforced, highlighting the necessity of implementing offline redundancies, defining threshold-based triggers, and precisely aligning hardware capabilities with the overall project scope.

---
