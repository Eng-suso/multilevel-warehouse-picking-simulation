#  Simulation of a Warehouse Logistic System with Multi-Level Picking

> Bachelor's Thesis in Industrial Engineering — University of Genova, Scuola Politecnica (DIME)
>
> **Author:** Sohayb Raqaq — **Supervisor:** Prof. Enrico Zero — **Year:** February 2026

---

##  Overview

This repository contains the simulation model developed as part of the Bachelor's thesis in Industrial Engineering.

The study analyzes an **automated four-level warehouse** using **Discrete Event Simulation (DES)**, with the goal of evaluating the impact of different AGV dispatching policies on overall system performance, with particular focus on vertical flows (lifts) and multi-level congestion.

### Main Objectives

- Model a multi-level logistics system with AGVs and lifts in AnyLogic
- Compare two AGV mission assignment policies:
  - **Nearest to agent** — selects the geometrically closest AGV to the pickup point
  - **Shortest path to pickup location** — selects the AGV with the shortest path to the pickup point
- Analyze KPIs related to throughput times, resource utilization, and vertical congestion

---

##  Repository Structure

```
 multilevel-picking-simulation
 ┣  simulazione_picking.alp   # AnyLogic model (DES)
 ┣ Raqaq_Sohayb_L_Gest.pdf  # Full thesis document
 ┗ README.md
```

---

## 🔧 System Requirements

| Requirement | Details |
|---|---|
| **Software** | [AnyLogic](https://www.anylogic.com/) 8.x or higher |
| **AnyLogic License** | Personal Learning Edition (PLE) or higher |
| **Operating System** | Windows / macOS / Linux |
| **Recommended RAM** | 8 GB or more |
| **AnyLogic Libraries** | Process Modeling Library (PML), Material Handling Library (MHL) |

>  The `.alp` file can only be opened with AnyLogic. The **free PLE version** is sufficient to open and run the model, but may have limitations on the number of simulated agents.

---

##  How to Run the Model

1. **Download and install AnyLogic** from the official website: [https://www.anylogic.com/downloads/](https://www.anylogic.com/downloads/)

2. **Clone the repository** or download the `.alp` file directly:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```

3. **Open AnyLogic** and go to `File → Open` to load the file `simulazione_picking.alp`

4. **Select the dispatching policy** inside the `Retrieve` block of the Material Handling Library:
   - `Nearest to agent`
   - `Shortest path to pickup location`

5. **Run the simulation** by pressing  in the toolbar

6. **Monitor the KPIs** directly in the model's graphical interface (AGV stack chart, lift time plots, throughput time histograms)

---

##  Model Description

### Warehouse Layout

- **4 floors** (P0 → P3) with racks and aisles
- **~1,000 items** with random location assignment
- **2 lifts** (Lift and Lift1) with FIFO discipline, both serving all floors
- **8 AGVs** with free space navigation
- **2 AGV parking stations** on floor P0
- **Order deposit area** on floor P0 with an unloading conveyor

### AnyLogic Libraries Used

| Library | Purpose |
|---|---|
| **Process Modeling Library (PML)** | Process flow logic (Source, Delay, Sink, TimeMeasureStart/End) |
| **Material Handling Library (MHL)** | Storage, AGV movement, lifts (Store, Retrieve, TransporterFleet) |
| **Space Markup** | Physical 2D/3D multi-level layout |

---

## 📊 KPIs Analyzed

| KPI | Description |
|---|---|
| **Order throughput time** | From mission activation to item unloading at the deposit area |
| **AGV operational utilization** | Percentage breakdown of AGV activity phases (idle, to item, transport, return) |
| **Lift utilization rate** | Fraction of time each lift is busy (0–1 scale) |
| **Number of lift calls per floor** | Frequency of lift access requests per floor level |
| **Cumulative vertical waiting time** | Total AGV waiting time in lift queues |

---

## 📈 Results Summary

| KPI | Shortest Path | Nearest to Agent | Best |
|---|---|---|---|
| Order throughput time | 9,447 s | **9,135 s** | ✅ Nearest |
| Total vertical waiting time | 10,114 s | **10,109 s** | ≈ equivalent |
| Waiting time on Lift1 (bottleneck) | 7,174 s | **6,500 s** | ✅ Nearest |
| Lift1 utilization rate | 0.41 | **0.34** | ✅ Nearest |
| Waiting time on Lift | **2,940 s** | 3,609 s | ✅ Shortest (trade-off) |

**Conclusion:** The *Nearest to agent* policy proves overall more effective: it reduces order lead time and relieves the most critical vertical resource (Lift1), redistributing congestion more evenly between the two lifts.

---

##  Reference

The full thesis, including literature review, methodology, and result analysis, is available in the file `Raqaq_Sohayb_L_Gest.pdf`.

---

##  Author

**Sohayb Raqaq**
Bachelor's Degree in Industrial Engineering
University of Genova — Scuola Politecnica (DIME)
February 2026

*Supervisor: Prof. Enrico Zero*
