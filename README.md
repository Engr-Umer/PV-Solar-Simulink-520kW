# 520 kW Grid-Connected PV Microgrid with MPPT & Battery Energy Management System

A MATLAB/Simulink (Simscape Electrical — Specialized Power Systems) study of a utility-scale, three-inverter photovoltaic plant with real Perturb-and-Observe MPPT control, verified against closed-form power electronics theory at every stage — paired with a 24-hour rule-based battery/demand-scheduling Energy Management System (EMS) built for a Pakistani residential Time-of-Use tariff.

> Full research article with title page, table of contents, glossary, component explanations, flowcharts, and clearly marked placeholders for your own circuit diagrams/graphs: [`report/PV_Microgrid_EMS_Technical_Report.docx`](report/PV_Microgrid_EMS_Technical_Report.docx) (22 pages)

---

## What's in this repo

| File | Description |
|---|---|
| `models/pv_520kw_microgrid.slx` | Circuit-level plant model — 3× PV → boost → MPPT → 3-phase inverter → filter → transformer chains on a shared AC bus |
| `models/ems_battery_scheduler.slx` | 24-hour signal-level EMS model — PV/load/tariff profiles, battery SOC tracker, rule-based scheduling controller |
| `report/` | Full technical report (.docx) and generated figures |
| `figures/` | Standalone PNG figures (topology diagrams, simulation results) |

---

## System overview

Three independent PV → boost-converter → MPPT chains feed a shared three-phase AC bus through individual inverters, filters, and an isolating step-up transformer:

![Plant architecture](figures/08_plant_architecture.png)

Each chain follows this signal path:

![Single chain topology](figures/07_single_chain_topology.png)

**PV array modeling** uses real Jinko Solar Tiger Neo N-type 78HL4 615 W module datasheet parameters (Voc = 56.25 V, Isc = 13.8 A, Vmp = 46.81 V, Imp = 13.14 A) — not idealized defaults — split across mixed 20-module and 19-module string groups per inverter to hit a combined **520.3 kW design target**:

| Inverter | Strings (20-mod / 19-mod) | Target Power |
|---|---|---|
| 1 | 4 / 11 | 177.7 kW |
| 2 | 3 / 12 | 177.1 kW |
| 3 | 3 / 11 | 165.4 kW |
| **Total** | **44 strings** | **520.3 kW** |

---

## Verification methodology

Every subsystem was validated against theory or cross-checked independently, not just simulated and accepted:

- **Boost converter (CCM):** measured output voltage matched the ideal `Vout = Vin/(1−D)` relation to within **0.05–2.7%** across multiple operating points. An initial discontinuous-conduction-mode (DCM) fault was diagnosed from a formula mismatch and corrected by resizing the inductor (0.5 mH → 5 mH).
- **MPPT convergence:** verified with a controlled irradiance step (1000 → 600 W/m²) mid-simulation — array voltage and power both re-tracked cleanly to a new steady-state operating point, confirming genuine closed-loop control rather than a fixed guess.
- **AC power delivery:** cross-checked using two independent methods — the Simscape `Power (vabc, iabc)` measurement block, and manual calculation from RMS voltage/current (`S = √3·V·I`) — agreeing within ~4%.
- **Grid-connection fault (documented, not hidden):** an early attempt to connect the inverter directly to an ideal grid source (before synchronization control existed) produced fault-level currents. This was correctly root-caused to a voltage/frequency/phase mismatch between two unsynchronized "stiff" sources — the same reason real substations require synchronization checks before paralleling generation. The model was validated against a local load instead; full grid PLL synchronization is noted as future work.

### Combined plant results

| Metric | Value |
|---|---|
| Combined DC array capacity (design) | 520.3 kW |
| Combined DC power (simulated) | ≈517–525 kW |
| AC active power delivered | ≈406 kW |
| Reactive power | ≈229 var (near-unity PF) |
| DC → AC conversion efficiency | ≈77% |

The ~77% efficiency (vs. the 95–98% typical of optimized commercial inverters) was root-caused to voltage drop across the output filter/transformer series impedance under load — documented as a known limitation and future optimization target, not a hidden or unexplained gap.

---

## Energy Management System (EMS)

A separate, discrete-time (1-minute resolution) 24-hour model studies battery dispatch and demand scheduling against a Pakistani residential Time-of-Use tariff:

![EMS architecture](figures/09_ems_architecture.png)

- **PV profile** — Islamabad solar timing (sunrise ≈5:30, solar noon ≈12:30, sunset ≈19:00)
- **Battery** — 2000 kWh, ±100 kW charge/discharge cap, SOC-limited (0–100%)
- **Tariff** — 30 PKR/kWh off-peak, 55 PKR/kWh during 17:00–22:00 peak
- **Flexible loads** — washing machine (1.5 kW), water-pump motor (0.75 kW), EV charger (3.3 kW), scheduled only during off-peak hours with sufficient SOC

### Results

![Battery SOC](figures/03_battery_soc.png)
![Cost comparison](figures/05_cost_comparison.png)

| Scenario | Net 24h Cost (PKR) |
|---|---|
| Smart scheduling (SOC + tariff aware) | −85,600 |
| Baseline (always-on) | −83,000 |
| **Net improvement** | **≈3%** |

Both scenarios net a cost credit due to the plant's large capacity relative to the household load modeled; the discussion in the full report covers the conditions (tighter storage, cloudier profiles, wider tariff spread) under which smart scheduling would show a larger advantage.

---

## Requirements

- MATLAB R2023a or later
- Simscape Electrical (Specialized Power Systems)
- Simulink

## Running the models

```matlab
% Circuit-level plant (switching-frequency resolution — slow, ~seconds to minutes per run)
open_system('models/pv_520kw_microgrid.slx')

% EMS study (1-minute resolution, 24h — runs in seconds)
open_system('models/ems_battery_scheduler.slx')
```

## Author

**Muhammad Umer Mujahid**
ACM Group of Industries

Built as part of graduate research preparation in power systems and renewable energy control. Full research article: [`report/PV_Microgrid_EMS_Technical_Report.docx`](report/PV_Microgrid_EMS_Technical_Report.docx)
