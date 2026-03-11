# 🛰️ LMS - Light My Satellite

**A Proof-of-Concept Distributed Mini-SLR Network for Global Space Debris Monitoring**

[![License: GNU](https://img.shields.io/badge/License-GNU-blue.svg)](LICENSE)
[![Hardware: Raspberry Pi](https://img.shields.io/badge/Hardware-Raspberry%20Pi%204-red.svg)](https://www.raspberrypi.org/)
[![Built for: НОИТ 2026](https://img.shields.io/badge/Built%20for-НОИТ%202026-green.svg)](https://edusoft.fmi.uni-sofia.bg/)

---

## 🌍 Vision: A Global Early Warning Network

**Imagine 1,000 tracking stations across the globe** — positioned at universities, schools, and amateur astronomy clubs — working together to monitor space debris in real time. Not to replace expensive precision systems, but to **complement them** with wide-area coverage that fills the critical blind spots in our current monitoring infrastructure.

**LMS and other mini SLR stations are the first step toward that vision.** This project demonstrates that satellite tracking technology doesn't need to cost millions. With accessible hardware and open-source software, we can build a distributed network that democratizes space situational awareness.

---

## 🚨 The Problem: Space is Getting Crowded

Over **170 million fragments** of space debris orbit Earth right now. With more than **12,000 active satellites** in Low Earth Orbit (88% of all satellites), the risk of catastrophic collisions grows daily. A single collision could trigger the **Kessler Syndrome** — a cascade of debris-generating impacts that could render entire orbital zones unusable for generations.

### Current Limitations
Traditional **Satellite Laser Ranging (SLR)** stations are the gold standard for tracking orbital objects:
- **~50 stations globally** — heavily concentrated in the Northern Hemisphere
- **$5-10 million per station** — prohibitively expensive for most organizations  
- **Significant blind spots** — especially in the Southern Hemisphere and equatorial regions  
- **Overloaded capacity** — existing stations struggle to keep pace with the growing number of objects

**We need more eyes on the sky. LMS makes that possible.**

---

## 💡 Our Solution: Affordable, Scalable, Distributed

LMS is a **proof-of-concept mini-SLR station** built with off-the-shelf components for **under $500**. While professional SLR systems achieve millimeter-level precision, LMS targets a different role in the ecosystem:

### Network Strategy
```
      ┌─────────────────────────────────┐
      │  Professional SLR Stations      │
      │  (Precision tracking & ranging) │
      │  ~50 stations | $5-10M each     │
      └────────────┬────────────────────┘
                   │
                   │ High-precision
                   │ follow-up
                   │
      ┌────────────▼────────────────────┐
      │  LMS Network (Early Detection)  │
      │  Wide-area coverage & alerting  │
      │  Target: 1000+ stations | $500  │
      └─────────────────────────────────┘
```

**Think of it as a pyramid:**
- **Top tier:** Precision SLR stations for detailed orbital determination
- **Base tier:** Thousands of LMS-like stations for detection, early warning, and continuous coverage

When an LMS station detects unexpected orbital changes, it alerts the nearest precision facility for detailed analysis.

---

## ✨ Current MVP Features

### Hardware Platform
- **4x TFmini-S LiDAR sensors** — organized in vertical and horizontal pairs for 3D positioning
- **Dual-axis tracking** — stepper motor (azimuth) + servo motor (elevation)
- **Raspberry Pi 4 controller** — handles sensor fusion, real-time tracking algorithms
- **Total cost: ~$500** (10,000x cheaper than traditional SLR)

### Real-Time Tracking System
- **Binary detection algorithm** — compares sensor pairs to determine target position
- **Independent axis control** — elevation and azimuth threads for responsive tracking
- **Automatic target acquisition** — initial scan followed by lock-on
- **Sub-degree accuracy** — sufficient for initial detection and handoff to precision systems

### Cloud Infrastructure
- **MQTT telemetry** — real-time sensor data streaming (20 measurements/sec)
- **InfluxDB time-series database** — optimized for high-frequency sensor data
- **Live 3D visualization** — browser-based Three.js rendering of tracked coordinates
- **Multi-tenancy architecture** — supports multiple stations and organizations

### Security Model
- **Write-only tokens** — stations can only publish to their own data bucket
- **ACL isolation** — MQTT broker enforces strict topic-level permissions
- **RAM-only credentials** — no sensitive tokens stored on disk
- **JWT authentication** — secure frontend access control

---

## 🏗️ Architecture

### System Overview
```
┌─────────────────────────────────────────────────────────────┐
│                    LMS Station (Hardware)                    │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │ LIDAR 1  │  │ LIDAR 2  │  │ LIDAR 3  │  │ LIDAR 4  │   │
│  │(Elev top)│  │(Elev bot)│  │(Azim L)  │  │(Azim R)  │   │
│  └─────┬────┘  └─────┬────┘  └─────┬────┘  └─────┬────┘   │
│        └──────────────┴──────────────┴──────────────┘       │
│                          │                                   │
│                   Raspberry Pi 4                             │
│              (Tracking algorithms + MQTT)                    │
└──────────────────────────┬──────────────────────────────────┘
                           │ MQTT/TLS
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                   Controller Platform                        │
│  ┌─────────────┐  ┌──────────────┐  ┌──────────────┐       │
│  │   Mosquitto │─▶│    Elysia    │◀─│   InfluxDB   │       │
│  │ MQTT Broker │  │   Backend    │  │  (TSDB)      │       │
│  └─────────────┘  └──────┬───────┘  └──────────────┘       │
│                           │ WebSocket                        │
│                           ▼                                  │
│                   ┌──────────────┐                           │
│                   │   Next.js    │                           │
│                   │   Frontend   │                           │
│                   │ (3D Viz)     │                           │
│                   └──────────────┘                           │
└─────────────────────────────────────────────────────────────┘
```

### Repository Structure
This project uses a multi-repository architecture:

- **[Didi0dum/LMS](https://github.com/Didi0dum/LMS)** (this repo) — Main integration hub & documentation
- **[rangelovkiril/lms-hardware](https://github.com/rangelovkiril/lms-hardware)** — Raspberry Pi station software (Python)
- **[rangelovkiril/lms-controller](https://github.com/rangelovkiril/lms-controller)** — Backend, frontend, MQTT broker & database (TypeScript/Bun)

---

## 🚀 Roadmap: From MVP to Global Network

### Phase 1: MVP ✅ (Current)
- [x] 4-LIDAR dual-axis tracking platform
- [x] Real-time coordinate streaming via MQTT
- [x] InfluxDB time-series storage
- [x] Live 3D browser visualization
- [x] Multi-station infrastructure support
- [x] Security model (tokens, ACL, JWT)

### Phase 2: Enhanced Detection (In Progress)
- [ ] Kalman filtering for noise reduction
- [ ] Velocity estimation and predictive tracking
- [ ] Automatic data quality assessment
- [ ] Weather station integration (temperature, humidity, cloud cover)
- [ ] Dockerized deployment (one-command setup)

### Phase 3: True SLR Capabilities (Future)
- [ ] **Pulsed laser emitter integration** — transition from passive LiDAR to active laser ranging
- [ ] **Retroreflector detection** — target satellites equipped with corner-cube retroreflectors
- [ ] **Time-of-flight measurement** — ns-precision timing for distance calculation
- [ ] **Orbit determination pipeline** — generate orbital elements from ranging data

### Phase 4: Network Intelligence (Vision)
- [ ] **TLE catalog integration** — compare live observations with predicted orbits (Space-Track API)
- [ ] **Anomaly detection** — automatic alerts when objects deviate from expected trajectories
- [ ] **Station coordination** — handoff between stations as objects move across the sky
- [ ] **Distributed orbit solving** — combine data from multiple stations for improved accuracy
- [ ] **Public dashboard** — global map of active stations and current detections

### Phase 5: Scale (Long-term Vision)
- [ ] **1,000+ station network** — strategic placement in underserved regions
- [ ] **Educational partnerships** — deployment at universities and astronomy clubs
- [ ] **Amateur astronomer integration** — open protocol for community contributions
- [ ] **ILRS coordination** — formal data sharing with International Laser Ranging Service

---

## 🛠️ Technology Stack

### Hardware
- **Raspberry Pi 4 Model B** — main controller (ARM Cortex-A72, 4GB RAM)
- **TFmini-S LiDAR** (4x) — ToF distance sensors (I²C, 12m range, ±5cm accuracy)
- **HY200-1607 Stepper Motor** — azimuth axis (200 steps/rev, 1:4 gearing)
- **A4988 Stepper Driver** — microstepping control (up to 1/16 step)
- **SG90 Micro Servo** — elevation axis (180° range, PWM control)

### Software - Station (Python)
- **Python 3.11+** — primary language
- **smbus2** — I²C communication with LiDAR sensors
- **pigpio** — hardware PWM for servo control
- **RPi.GPIO** — stepper motor control
- **paho-mqtt** — telemetry streaming

### Software - Controller (TypeScript)
- **Bun** — JavaScript runtime (4x faster than Node.js)
- **Elysia** — lightweight web framework
- **Next.js** — frontend with SSR
- **Three.js** — WebGL 3D visualization
- **InfluxDB** — time-series database (90x compression for sensor data)
- **Mosquitto** — MQTT broker with ACL support

---

## 📊 Performance Characteristics

### Current Capabilities
| Metric | Value | Notes |
|--------|-------|-------|
| **Detection Range** | 0.01 - 12 meters | LiDAR hardware limitation |
| **Angular Accuracy** | ~0.5° | Combined servo + stepper error |
| **Update Rate** | 20 Hz | Per-axis measurement frequency |
| **Data Throughput** | 1 KB/sec/station | Sustainable with 1000 stations |
| **Tracking Latency** | <100 ms | Sensor read → decision → actuation |

### Theoretical LEO Performance
For a satellite at 400 km altitude:
- **5 cm ranging error** → **0.007° angular error** (acceptable for detection)
- **Detection window** → ~10 minutes (horizon to horizon at LEO)
- **Handoff coordination** → Alert precision station when object enters their FOV

### Scalability
- **1 station** → Local testing, algorithm development
- **10 stations** → Regional network, redundancy validation  
- **100 stations** → Continental coverage, anomaly detection
- **1,000 stations** → Global network, continuous monitoring

---

## 🎯 Why This Matters

### Scientific Impact
- **Fill blind spots** in existing SLR networks (Southern Hemisphere, equatorial zones)
- **Increase temporal coverage** — more frequent observations of critical objects
- **Enable rapid response** — distributed detection reduces time-to-alert

### Educational Value
- **Hands-on space science** — universities can deploy their own tracking station
- **STEM engagement** — tangible connection between orbital mechanics and hardware
- **Open-source learning** — complete codebase available for study and modification

### Economic Accessibility
- **10,000x cost reduction** compared to traditional SLR
- **Modular design** — upgrade components incrementally (LiDAR → laser, servo → precision mount)
- **Consumer hardware** — no specialized equipment or export restrictions

---

## 📖 Getting Started

### Quick Start (Full Documentation in Submodules)
```bash
# Clone main repository
git clone --recursive https://github.com/Didi0dum/LMS.git
cd LMS

# Hardware setup
cd lms-hardware
# See hardware/README.md for detailed assembly and configuration

# Controller setup
cd ../lms-controller
# See controller/README.md for Docker Compose deployment
```

### Prerequisites
- Raspberry Pi 4 (2GB+ RAM recommended)
- 4x TFmini-S LiDAR sensors
- Stepper motor + driver (A4988 or compatible)
- Servo motor (SG90 or similar)
- Docker + Docker Compose (for controller)

---

## 🤝 Contributing

We welcome contributions from:
- **Hardware enthusiasts** — alternative sensor configurations, mechanical improvements
- **Software developers** — algorithm optimization, new features, bug fixes
- **Astronomers** — orbital mechanics expertise, TLE integration
- **Educators** — curriculum development, documentation improvements

### Development Priorities
1. **Kalman filter implementation** — reduce noise, improve coordinate stability
2. **Weather integration** — correlate tracking quality with atmospheric conditions
3. **Simulation environment** — test algorithms without physical hardware
4. **Mobile app** — remote station monitoring and control

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 👥 Team

**Developed for НОИТ 2026 (National Olympiad in Information Technologies)**

- **Dilyana Vasileva** — Hardware architecture, sensor integration, tracking algorithms
- **Kiril Rangelov** — Backend infrastructure, real-time visualization, security model

**Supervisor:** Milen Spasov (TUES)

---

## 📚 References & Inspiration

- **miniSLR Stuttgart** — Low-budget SLR proof-of-concept ([Paper](https://elib.dlr.de/202724/))
- **ILRS Network** — International Laser Ranging Service ([ilrs.gsfc.nasa.gov](https://ilrs.gsfc.nasa.gov/))
- **Space-Track.org** — Public satellite catalog (TLE data)
- **ESA Space Debris Office** — Space debris statistics and research

---

## 📄 License

This project is licensed under the GNU License — see [LICENSE](LICENSE) file for details.

---

## 🌟 Acknowledgments

- **Benewake** — TFmini-S LiDAR documentation and support
- **InfluxData** — Time-series database guidance
- **Raspberry Pi Foundation** — Enabling accessible hardware prototyping
- **Open-source community** — Libraries and tools that made this possible

---

## 📬 Contact

- **Project Repository:** [github.com/Didi0dum/LMS](https://github.com/Didi0dum/LMS)
- **Hardware Module:** [github.com/rangelovkiril/lms-hardware](https://github.com/rangelovkiril/lms-hardware)
- **Controller Module:** [github.com/rangelovkiril/lms-controller](https://github.com/rangelovkiril/lms-controller)
- **Email:** dilyana.k.vasileva@gmail.com, kiril.l.rangelov.2022@elsys-bg.org

---

<div align="center">

**🛰️ Building a safer orbital environment, one station at a time.**

*"The best way to predict the future is to build it."* — Alan Kay

[![GitHub stars](https://img.shields.io/github/stars/Didi0dum/LMS?style=social)](https://github.com/Didi0dum/LMS/stargazers)
[![GitHub watchers](https://img.shields.io/github/watchers/Didi0dum/LMS?style=social)](https://github.com/Didi0dum/LMS/watchers)

</div>
