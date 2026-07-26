# 520 kW Grid-Connected PV Microgrid with MPPT & Battery Energy Management System

<p align="center">
  <img src="Image.png" alt="520 kW PV Microgrid" width="100%">
</p>

<p align="center">
  <b>MATLAB / Simulink · Simscape Electrical · Photovoltaic Systems · MPPT · Power Electronics · Battery EMS · Smart Energy Management</b>
</p>

---

## 📌 Project Overview

This repository presents the design, simulation, verification, and analysis of a **520 kW-class photovoltaic (PV) microgrid** developed in **MATLAB/Simulink using Simscape Electrical — Specialized Power Systems**.

The project combines two major studies:

1. **A circuit-level 520 kW-class PV power conversion system**
2. **A 24-hour battery and demand-side Energy Management System (EMS)**

The PV plant consists of three independently modeled PV generation and power-conversion chains:

**PV Array → P&O MPPT → DC-DC Boost Converter → Three-Phase VSC Inverter → LC Filter → Transformer → AC Bus**

The EMS study integrates:

**PV Generation + Household Load + Battery Storage + Battery SOC + Time-of-Use Tariff + Flexible Appliance Scheduling**

The project follows a **verification-first engineering methodology**, where major subsystems are validated against theoretical equations, controlled test cases, and independent measurement methods.

---

## 🎯 Key Objectives

- Design a realistic **520 kW-class PV plant** using manufacturer datasheet parameters.
- Model three independent PV-to-AC inverter chains connected to a common AC bus.
- Implement a **Perturb-and-Observe (P&O) MPPT algorithm**.
- Design and verify a **DC-DC boost converter**.
- Convert regulated DC power into three-phase AC using a **Voltage Source Converter (VSC)**.
- Apply LC filtering to reduce inverter switching harmonics.
- Use a step-up/isolation transformer for AC-side voltage transformation.
- Verify subsystem performance using theoretical calculations and independent measurements.
- Test MPPT response under changing solar irradiance.
- Develop a 24-hour rule-based **Battery Energy Management System (EMS)**.
- Implement battery SOC-aware charging and discharging.
- Incorporate a Pakistan-specific residential **Time-of-Use (ToU) tariff**.
- Schedule flexible household loads according to tariff periods, PV availability, and battery SOC.

---

# ⚡ System Architecture

The overall PV power-conversion path is:

```text
Solar Irradiance
       │
       ▼
   PV Array
       │
       ▼
Voltage / Current Measurement
       │
       ▼
    P&O MPPT
       │
       ▼
DC-DC Boost Converter
       │
       ▼
     DC Bus
       │
       ▼
Three-Phase VSC Inverter
       │
       ▼
    LC Filter
       │
       ▼
Step-Up / Isolation Transformer
       │
       ▼
     AC Bus
       │
       ├──────────► Local Load
       │
       └──────────► Grid Interface
