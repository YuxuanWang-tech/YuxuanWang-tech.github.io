---
layout: page
title: Numerical Simulations of He-Accretion on 1.25 Msun ONe WDs
description: This project investigates the long-term evolution and nucleosynthetic yields of **Helium Novae**. Using the **MESA (v.r23.05.1)** code, we simulate a $1.25 M_{\odot}$ Oxygen-Neon White Dwarf accreting helium at a constant rate of $\dot{M} = 10^{-7} M_{\odot}/\text{yr}$.
importance: 3
category: Work
enable_mathjax: true
---

## 1. Project Overview

The core objective is to identify **isotopic fingerprints** (such as $^{12}\text{C}/^{13}\text{C}$ and $^{14}\text{N}/^{15}\text{N}$) that distinguish helium-burning novae from classical hydrogen-burning novae.

---

## 2. Experimental Setup & Technical Details
### Model Configuration
- **Core Model:** `o_ne_wd.mod` (1.25 Solar Masses)
- **Nuclear Network:** `approx21.net` (Tracing $\alpha$-chain and CNO isotopes)
- **Accretion Species:** Pure $^4\text{He}$ ($Y=1.0$)

### Numerical Strategies (Overcoming the 81,640 "Wall")
During the simulation, the model encountered severe convergence issues at the onset of Thermonuclear Runaway (TNR). To bridge the gap between quasi-static accretion and dynamic eruption, the following numerical "surgery" was performed:

| Parameter | Baseline Value | Adjusted Value | Purpose |
| :--- | :--- | :--- | :--- |
| `varcontrol_target` | $10^{-4}$ | $10^{-3}$ | Relaxing solver tolerance to avoid infinite retries during peak flash. |
| `mesh_delta_coeff` | $0.5$ | $1.5$ | Coarsening the grid to handle the rapidly expanding envelope ($R \approx 1.3 R_{\odot}$). |
| `max_num_photos` | $10$ | $200$ | Increasing backup frequency to prevent data loss from system crashes. |

---

## 3. Preliminary Results
### Quasi-Steady Burning Phase
At Step $\sim 77,000$, the WD reached a critical stability point:
- **Nuclear Luminosity:** $\log(L_{\text{nuc}}/L_{\odot}) \approx 5.27$
- **Peak Temperature:** $\log(T_{\text{max}}/\text{K}) \approx 8.91$ (Over 800 million K)
- **Envelope Radius:** Expanded from WD-scale to $\sim 1.3 R_{\odot}$.

---

## 4. Discussion: MESA vs. SHIVA
A key takeaway from this stage is the limitation of 1D hydrostatic codes like MESA in the late stages of TNR. 
- **MESA:** Excellent for the 13-million-year accretion history.
- **SHIVA:** More robust for the explosive hydrodynamic phase (shocks and mass ejection).

**Future Work:** We plan to use the MESA profile at $L_{\text{nuc}}$ peak as a "hand-off" model for **SHIVA** to obtain high-fidelity nucleosynthetic yields.

---

## 5. Visualizing the Evolution
*Below is a placeholder for the Python-generated plot (nova_analysis_81k.png) showing the luminosity plateau and temperature rise.*

![Nova Evolution Plot](your_image_path/nova_analysis_81k.png)

---

## 6. How to Run
To reproduce the pre-flash state:
1. Load `inlist_project`.
2. Ensure `history_columns.list` has `add_average_abundances` enabled.
3. Run `./re x600` (or your latest checkpoint).

```bash
# Example restart command
export OMP_NUM_THREADS=8
./re x600