--- 
layout: page 
title: "Project 3: Chasing the Chandrasekhar Limit — Overcoming Numerical Collapses in MESA" 
description: "A technical deep dive into generating extreme-mass White Dwarfs (1.35 M_sun) for Helium Nova simulations, balancing mathematical solvers with fundamental physics." 
img: assets/img/7.jpg 
importance: 3 
category: Work 
--- 
 
# Chasing the Chandrasekhar Limit: A MESA Logbook 
 
Generating an extreme-mass White Dwarf (1.35 M_sun) as the progenitor for Helium Nova simulations is not as simple as tweaking a mass parameter. It is a battle against both numerical limits and fundamental astrophysics.  
 
In **Project 3 (HeNova-DB)**, I documented the engineering challenges and physical workarounds required to stabilize implicit hydrodynamics solvers when pushing degenerate matter to the edge of the Chandrasekhar limit. 
 
## 1. The "CO WD" Illusion & The Solver Wall 
 
Initially, the goal was to inflate a standard 0.96 M_sun Carbon-Oxygen (CO) White Dwarf to 1.35 M_sun using MESA's mathematical `relax_mass` module. However, pushing a CO core to this limit triggered a series of catastrophic solver crashes.  
 
Here is a breakdown of the three major failure states and their underlying causes: 
 
### Crash A: The Opacity Blindspot 
When loading a bare WD model without its evolutionary history, the system lacks the baseline metallicity for the opacity tables. 
> **Error:** `must supply Zbase for Type2 opacities -1.0000000000000000D+00` 
 
**Diagnosis & Fix:** The Type 2 opacity tables (necessary for CO-rich environments) require a defined reference. Explicitly defining the solar metallicity baseline in the `&kap` namelist resolved the initialization failure: 
```fortran 
&kap 
      Zbase = 0.02d0 
      use_Type2_opacities = .true. 
```

### Crash B: Compressional Heating vs. Implicit Solvers 
Using `relax_mass` to artificially inject mass into a degenerate object causes extreme gravitational contraction. The compressional heating forces the implicit solver (Newton-Raphson) to shrink the timestep (`dt`) exponentially to maintain hydrostatic equilibrium, eventually hitting the hard-coded floor. 
> **Error:** `stopping because of problems dt < min_timestep_limit (9.99D-07)` 
 
**Diagnosis & Fix:** The accretion rate was too violent for the solver to resolve the surface density gradients. The fix involved relaxing the timestep limits to microscopic scales (`min_timestep_limit = 1d-12`), lowering mesh resolution requirements (`mesh_delta_coeff = 2.0`), and implementing a slow "Cold Accretion" strategy. 
 
### Crash C: The Adiabatic Expansion Freeze 
To prevent fake "supernovae" caused by the aforementioned compressional heating, nuclear reactions were forcefully disabled (`eps_nuc_factor = 0`). However, forced mass addition combined with structural reorganization caused adiabatic expansion in the outer layers, plunging the temperature below the matrix's mathematical limits. 
> **Error:** `retry: logT < hydro_mtx_min_allowed_logT` 
 
**Diagnosis & Fix:** You cannot violate the Virial Theorem. Suppressing fusion while violently altering gravity breaks the thermodynamic state of the gas, causing the solver matrix to become ill-conditioned. A physical pivot was necessary. 
 
## 2. The Physical Reality: Pivoting to ONe WDs 
 
The ultimate conclusion was a triumph of physics over mathematical "hacks": **A 1.35 M_sun CO White Dwarf does not exist in nature.** At roughly 1.05 to 1.1 M_sun, the core density and temperature become high enough to trigger Carbon Ignition. Therefore, any realistic 1.35 M_sun progenitor for a cataclysmic variable must inherently be an Oxygen-Neon (ONe) White Dwarf. Fighting the solver was merely a symptom of fighting fundamental physics. 
 
## 3. The "Six-Stage Rocket" Solution 
 
Instead of artificially hacking a small stellar remnant, the pipeline was restructured to use MESA's `make_o_ne_wd` suite, evolving a massive star from the Zero Age Main Sequence (ZAMS) all the way to its death. 

### The Pipeline Architecture 
* **`inlist_zams`**: Ignite a massive ZAMS star. 
* **`inlist_to_agb`**: Evolve the star to the Asymptotic Giant Branch. 
* **`inlist_remove_envelope`**: Numerically strip the enormous H/He envelope (simulating extreme stellar winds). 
* **`inlist_c_burn`**: The critical carbon flash stage. 
* **`inlist_o_ne_wd`**: Cooling and settling into the final compact object. 
 
### Forging the 1.35 M_sun Core 
To achieve the absolute upper limit of WD mass, the initial main-sequence mass was scaled up from the standard 11 M_sun to 12.5 M_sun. Furthermore, pre-compiled standard models (`standard_*.mod`) were actively bypassed to force a complete, un-interpolated numerical simulation: 

```fortran 
&controls 
      initial_mass = 12.5d0  
      initial_z = 0.02d0   
       
      ! Uncapping the step limit for extreme evolution tracking 
      max_model_number = -1  
```
# Conclusion & Next Steps

By respecting the physical boundaries of stellar evolution rather than forcing numerical solutions upon unstable configurations, the pipeline successfully generated a physically sound, stable 1.35 M_sun ONe White Dwarf.

This extreme object now serves as the foundational database for the next phase of the HeNova-DB project: simulating stable cold accretion (Helium mass transfer from a binary companion) and extracting the time-series data of the ensuing thermonuclear runaway.
/