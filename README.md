# Smart-Wearable-Device-for-Parkinson-s-Patient-Monitoring-System
# Smart Wearable Device for Parkinson's Patient Monitoring System

A low-cost, wearable IoT system that continuously monitors hand tremor and gait
patterns using motion and pressure sensors, and applies a machine learning model
to classify a patient's condition as normal or Parkinson's-affected in real time
— with automatic local and remote alerts on abnormal or fall detection.

**Major Project (2025–2026) — Department of ECE, Anurag University**

---

## Table of Contents
- [Problem Statement](#problem-statement)
- [Objectives](#objectives)
- [System Architecture](#system-architecture)
- [Hardware Components](#hardware-components)
- [Software & Libraries](#software--libraries)
- [Circuit / Pin Connections](#circuit--pin-connections)
- [Dataset](#dataset)
- [How It Works](#how-it-works)
- [Results](#results)
- [Applications](#applications)
- [Future Scope](#future-scope)
- [References](#references)
- [Team](#team)

---

## Problem Statement
Parkinson's disease is a progressive neurological disorder that affects motor
functions such as hand tremors and gait, increasing the risk of falls and
disrupting daily activities. Existing diagnosis and monitoring methods are
mostly hospital-based and periodic, which means they don't support continuous,
real-time tracking of symptoms — making early detection and timely intervention
difficult in everyday life. In India alone, Parkinson's affects an estimated
5–6 lakh people, a number expected to grow with an aging population. This
project addresses the need for a low-cost, wearable, and intelligent system for
continuous symptom monitoring.

## Objectives
- Design a wearable system to monitor hand tremor and leg movement in Parkinson's patients
- Collect real-time motion data using sensors and process it with an embedded controller
- Extract and analyze motion features related to tremor and gait from sensor data
- Apply machine learning to classify a person as normal or Parkinson's-affected
- Generate alerts during abnormal or critical conditions

## System Architecture
Sensor Modules (MPU6050, FSR x2)
│
▼
ESP32 Microcontroller (live sensor reading + Wi-Fi transmission)
│
▼
ML Model — Random Forest (condition classification)
│
▼
Condition Output: Normal / Parkinson's
│
▼
Buzzer Alert (local) + Telegram Notification (remote caregiver)


Sensors attached to the hand and leg collect motion and pressure data, which the
ESP32 transmits over Wi-Fi to a Flask server. There, a Random Forest model
analyzes the data and classifies the subject's condition. If a fall or critical
abnormal condition is detected, a buzzer sounds locally and a Telegram alert is
sent to notify a caregiver remotely.

## Hardware Components
| Component | Purpose |
|---|---|
| ESP32 Microcontroller | Data acquisition, preprocessing, and Wi-Fi communication |
| MPU6050 (IMU) | Hand tremor motion sensing (accelerometer + gyroscope) |
| FSR Sensors (x2) | Foot pressure / gait sensing (heel + toe) |
| Buzzer | Local alert for fall or critical condition |
| 18650 Battery + TP4056 Module | Portable power supply with charging support |
| ON/OFF Switch | Power control |

## Software & Libraries
| Tool | Role |
|---|---|
| Arduino IDE | Programming the ESP32 |
| Python | ML model training, testing, and serving |
| Scikit-learn | Random Forest classification algorithm |
| Pandas / NumPy | Data handling and preprocessing |
| Joblib | Saving/loading the trained ML model |
| Flask | Serving the model and handling real-time predictions |
| Telegram API | Remote caregiver alerting |

## Circuit / Pin Connections
| Sensor | Pin on Sensor | Connected to ESP32 |
|---|---|---|
| MPU6050 | SDA | GPIO21 |
| MPU6050 | SCL | GPIO22 |
| MPU6050 | GND | GND |
| FSR1 (heel) | OUT | GPIO34 |
| FSR1 (heel) | GND | GND |
| FSR2 (toe) | OUT | GPIO35 |
| FSR2 (toe) | GND | GND |
| Buzzer | Signal | GPIO25 |
| Power | 18650 + TP4056 | 5V → 3.3V regulated rail |

## Dataset
A feature-level fusion dataset combining tremor and gait indicators.

- **Samples:** 3,001
- **Format:** CSV
- **Label:** 0 = Healthy, 1 = Parkinson's

| Feature | Description |
|---|---|
| ax, ay, az | Acceleration in X/Y/Z — hand movement intensity and variation |
| gx, gy, gz | Angular velocity in X/Y/Z — tremor rotation, frequency, and instability |
| Fsr1 | Foot pressure at heel region |
| Fsr2 | Foot pressure at toe region |

## How It Works
1. Wearable sensors on the hand and leg continuously collect motion and pressure data
2. The ESP32 preprocesses and extracts tremor/gait features from the raw sensor readings
3. Data is transmitted over Wi-Fi to a Flask server
4. A Random Forest model (trained on the 3,001-sample dataset) classifies the condition
5. On a normal reading, no action is taken; on an abnormal/fall condition, a buzzer
   triggers locally and a Telegram alert is sent to a caregiver

## Results
- Reliable, high-confidence classification validated through hardware prototype
  testing across both normal and abnormal conditions
- Combining multiple sensors (tremor + gait) improved detection accuracy over
  single-sensor approaches
- Real-time Wi-Fi + Telegram alerting enabled fast response to critical conditions

## Applications
- Continuous home-based Parkinson's monitoring
- Elderly care and fall detection
- Rehabilitation centers
- Remote patient supervision for caregivers and clinicians

## Future Scope
- Expand the dataset with more diverse patient samples to improve generalization
- Add additional sensor modalities (e.g., EMG) for richer feature extraction
- Move from Wi-Fi-only to a hybrid Wi-Fi/BLE setup for better range and battery life
- Build a caregiver-facing dashboard for historical trend tracking

## References
1. Z. Zheng et al., "Inertial measurement units for early gait recognition of Parkinson's disease using ensemble learning," IEEE Access, vol. 12, 2024.
2. R. Hua et al., "Toe tapping–based falling risk evaluation for patients with Parkinson's disease using monitoring insoles," IEEE Sensors Journal, vol. 22, no. 6, 2022.
3. H. Mughal et al., "Parkinson's disease management via wearable sensors: A systematic review," IEEE Access, vol. 10, 2022.
4. M. Sica et al., "Design of a multi-sensors wearable system for continuous home monitoring of people with Parkinson's disease," IEEE Access, vol. 12, 2024.
5. K. Velu and N. Jaisankar, "Design of an early prediction model for Parkinson's disease using machine learning," IEEE Access, vol. 13, 2025.

## Team
Built by Batch A19, Department of ECE, Anurag University — under the guidance of
Dr. Laxma Reddy, Assistant Professor, Dept. of ECE.
