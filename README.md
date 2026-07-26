# ⚡ 520 kW Grid-Connected PV Microgrid with MPPT & Battery Energy Management System

<p align="center">
  <img src="Image.png" alt="520 kW PV Microgrid" width="100%">
</p>

<p align="center">
  <b>A MATLAB/Simulink-based study of a 520 kW-class photovoltaic microgrid with P&O MPPT, power electronic conversion, battery storage, and intelligent Energy Management System (EMS).</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/MATLAB-R2023a%2B-orange?style=for-the-badge&logo=mathworks" alt="MATLAB">
  <img src="https://img.shields.io/badge/Simulink-Simscape%20Electrical-blue?style=for-the-badge" alt="Simulink">
  <img src="https://img.shields.io/badge/PV%20Capacity-520.3%20kW-green?style=for-the-badge" alt="PV Capacity">
  <img src="https://img.shields.io/badge/MPPT-P%26O-yellow?style=for-the-badge" alt="MPPT">
  <img src="https://img.shields.io/badge/EMS-Battery%20%2B%20ToU-purple?style=for-the-badge" alt="EMS">
</p>

---

# 📌 Overview

This repository presents the **design, modeling, simulation, verification, and analysis of a 520 kW-class photovoltaic (PV) microgrid** developed in **MATLAB/Simulink using Simscape Electrical — Specialized Power Systems**.

The project combines two interconnected research studies:

### ☀️ 1. Circuit-Level PV Microgrid

A detailed PV power-conversion system consisting of:

**PV Arrays → P&O MPPT → DC-DC Boost Converters → DC Link → Three-Phase VSC Inverters → LC Filters → Transformers → AC Bus**

### 🔋 2. Battery Energy Management System

A separate 24-hour discrete-time Energy Management System integrating:

**PV Generation + Household Demand + Battery Storage + Battery SOC + Time-of-Use Tariff + Flexible Load Scheduling**

The project follows a **verification-first engineering methodology**. Major subsystems are not simply simulated and accepted; instead, their behavior is cross-checked using theoretical equations, controlled test cases, and independent measurement methods.

---

# 🖼️ Project Overview

<p align="center">
  <img src="00_cover_icon.png" alt="Project Overview" width="850">
</p>

---

# 🎯 Project Objectives

The main objectives of this project are to:

- Design a realistic **520 kW-class photovoltaic power plant**.
- Use real manufacturer datasheet parameters for PV module modeling.
- Develop three independent PV power-conversion chains.
- Implement a custom **Perturb-and-Observe (P&O) MPPT** algorithm.
- Design and verify DC-DC boost converters.
- Convert regulated DC power into three-phase AC using Voltage Source Converters.
- Apply LC filtering to improve AC waveform quality.
- Model step-up/isolation transformers.
- Validate power-electronics subsystems using theoretical calculations.
- Test MPPT performance under changing solar irradiance.
- Investigate and diagnose simulation faults.
- Develop a 24-hour rule-based Battery Energy Management System.
- Model battery State of Charge (SOC) behavior.
- Incorporate a Pakistan-specific Time-of-Use (ToU) tariff.
- Schedule flexible household appliances based on tariff, PV availability, and battery SOC.
- Compare smart scheduling against a baseline operating strategy.

---

# ⚡ Complete System Architecture

The overall PV power-conversion architecture is shown below.

<p align="center">
  <img src="08_plant_architecture.png" alt="520 kW PV Plant Architecture" width="950">
</p>

The complete energy conversion path is:

```text
                    SOLAR IRRADIANCE
                           │
                           ▼
                      PV ARRAYS
                           │
                           ▼
                Voltage / Current Measurement
                           │
                           ▼
                       P&O MPPT
                           │
                           ▼
                 DC-DC BOOST CONVERTER
                           │
                           ▼
                        DC LINK
                           │
                           ▼
                THREE-PHASE VSC INVERTER
                           │
                           ▼
                       LC FILTER
                           │
                           ▼
               STEP-UP / ISOLATION
                    TRANSFORMER
                           │
                           ▼
                        AC BUS
                       /      \
                      /        \
                     ▼          ▼
                LOCAL LOAD    GRID
