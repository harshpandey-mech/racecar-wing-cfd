# Race Car Aerodynamic Wing — CFD Study
### SOLIDWORKS + ANSYS Fluent | RANS k-ε | Downforce & Drag Optimization

---

## 📌 Project Overview

This project performs a **full Computational Fluid Dynamics (CFD) analysis** of a two-element rear wing assembly for a Formula Student–class race car. The study evaluates aerodynamic performance across a range of flap angles and angles of attack, with the goal of maximising downforce while minimising drag penalty.

The simulation uses **steady-state RANS (k-ε turbulence model)** in ANSYS Fluent — the same approach used in professional motorsport aerodynamic development.

---

## 🎯 Objectives

- Evaluate lift (CL) and drag (CD) coefficients across geometric configurations
- Study pressure distribution and flow separation on the wing surfaces
- Identify optimal flap angle and angle of attack for best L/D ratio
- Compare two-element wing performance against single-element baseline

---

## ⚙️ Methodology

### Geometry — Two-Element Rear Wing
- **Mainplane:** NACA 4412 aerofoil profile, chord = 250 mm
- **Flap:** High-camber element, chord = 120 mm
- **Span:** 1200 mm (representative Formula Student rear wing)
- **Endplates:** Included in full 3D model
- CAD modelled in **SOLIDWORKS**, exported as STEP for Fluent meshing

### CFD Setup — ANSYS Fluent
| Parameter | Value |
|---|---|
| Solver | Pressure-based, steady-state |
| Turbulence Model | Realizable k-ε with enhanced wall treatment |
| Fluid | Air, ρ = 1.225 kg/m³, μ = 1.789×10⁻⁵ Pa·s |
| Inlet velocity | 50, 90, 130, 180 km/h |
| Outlet | Pressure outlet (0 Pa gauge) |
| Wing surfaces | No-slip wall |
| Domain | 10c upstream, 20c downstream, 8c height |

### Mesh Strategy
| Mesh Region | Cell Count | y⁺ Target |
|---|---|---|
| Coarse (sensitivity check) | 1.2M | ~15 |
| Medium | 2.4M | ~5 |
| Fine (production runs) | 3.8M | ≤ 5 |

Inflation layers applied at all wall boundaries. Mesh sensitivity study confirmed results were grid-independent at 3.8M cells (< 1.2% change from 2.4M mesh).

### Parametric Sweep
- **Flap angle:** 15°, 20°, 25°, 28°, 30°, 35°
- **Mainplane AoA:** 5°, 8°, 11°, 14°, 17°, 20°

---

## 📊 Results

### Optimal Configuration
| Parameter | Value |
|---|---|
| Flap angle | **28°** |
| Mainplane AoA | **14°** |
| Lift coefficient CL | **1.74** |
| Drag coefficient CD | **0.31** |
| Lift-to-Drag ratio (L/D) | **5.6** |
| Downforce improvement vs. baseline single-element | **+22%** |
| Drag increase vs. baseline | **+9%** |

### Performance Across Speed Range (Optimal Config)
| Speed (km/h) | Downforce (N) | Drag (N) |
|---|---|---|
| 50 | 58 | 10 |
| 90 | 188 | 34 |
| 130 | 392 | 70 |
| 180 | 752 | 134 |

**Key Finding:** Flow separation was observed at flap angles above 30°, causing a sharp CL drop (stall). The 28° configuration sits just below the stall boundary, providing maximum attached-flow downforce. Beyond 14° mainplane AoA, the suction-side boundary layer began separating near the trailing edge — confirming 14° as the upper limit for efficient operation.

---

## 📁 Repository Structure

```
racecar-wing-cfd/
│
├── README.md
│
├── geometry/
│   ├── wing_assembly.SLDPRT       # SOLIDWORKS part file
│   ├── wing_assembly.STEP         # STEP export for ANSYS import
│   └── wing_dimensions.pdf        # Annotated drawing with all dimensions
│
├── fluent_setup/
│   ├── mesh_settings.md           # Exact mesh parameters to reproduce
│   ├── boundary_conditions.md     # All BC values and settings
│   └── solver_settings.md         # Residual targets, relaxation factors
│
├── results/
│   ├── CL_CD_vs_flap_angle.png
│   ├── pressure_contour_optimal.png
│   ├── velocity_streamlines.png
│   ├── mesh_sensitivity_study.png
│   └── parametric_sweep_summary.png
│
└── data/
    └── results_summary.xlsx        # All CL, CD values for all configurations
```

> **Note:** ANSYS Fluent `.cas` and `.dat` files are not included due to file size. Full setup instructions are documented in `fluent_setup/` — results are fully reproducible following those steps.

---

## 🔧 Software Required

- SOLIDWORKS 2021 or later (geometry)
- ANSYS Fluent 2021 R1 or later (CFD solver)

---

## 📚 References

- Anderson, J.D. — *Introduction to Flight*, 8th Ed.
- Katz, J. — *Race Car Aerodynamics*, Bentley Publishers
- ANSYS Fluent Theory Guide — Realizable k-ε model formulation
- Formula Student Germany — Technical Regulations (aerodynamic component reference)

---

## 👤 Author

**Harsh Pandey**  
B.Tech Mechanical Engineering, IET Lucknow (AKTU)  
📧 harshpanddey1881@gmail.com 
