# Weldpoly App — Calculation Formulas

All formulas currently hardcoded in the app. Please review and flag anything that needs correction.

---

## Inputs (entered by user)

| Input | Description |
|---|---|
| **OD** | Pipe outside diameter (mm) — selected from list |
| **SDR** | Standard Dimension Ratio — selected from list |
| **Drag** | Drag pressure (Bar) — entered manually |
| **Welding Standard** | ISO 21307 Low Pressure Fusion (LP) /High Pressure Fusion (HP), or DVS 2207 |
| **Machine** | Selected from machine list |

**Available OD sizes (mm):**
40, 50, 63, 75, 90, 110, 125, 140, 160, 180, 200, 225, 250, 280, 315, 355, 400, 450, 500, 560, 630, 710, 800, 900, 1000, 1200, 1400, 1600, 1800, 2000, 2250, 2500

**Available SDR values:** 7.4, 9, 11, 13.6, 17, 21, 26, 41

---

## Step 1 — Wall Thickness

| Standard | Formula |
|---|---|
| ISO 21307 (LF and HF) | `wallThickness = ROUND(OD / SDR)` mm |
| DVS 2207 | `wallThickness = OD / SDR` mm *(not rounded)* |

---

## Step 2 — Interfacial Surface Area

All standards:

```
interfacialArea = π × (OD − wallThickness) × wallThickness    [mm²]
```

---

## Step 3 — Gauge Pressure (Bead-Up & Fusion Jointing Pressure)

```
gaugePressure = interfacialPressure × (interfacialArea / cylinderArea) × 10 + drag    [Bar]
The gauge pressure can be calculated from the following formula:
GP=(IPxAs/Acx10)+DP
where
GP is the gauge pressure (bar);
IP is the interfacial pressure (MPa);
Ac is the total piston area, given by the manufacturer of the butt fusion jointing equipment (mm2);
As is the interfacial surface area (mm2);
DP is the drag pressure (bar).
```

**Interfacial pressure constant** (from welding standard):

| Standard | Interfacial Pressure |
|---|---|
| ISO 21307 SP Low Fusion | **0.17 MPa** |
| ISO 21307 SP High Fusion | **0.52 MPa** |
| DVS 2207 | **0.15 MPa** |

> ⚠️ **Please verify:** Are these values correct for your applicable edition of the standards?
Yes
> 
**cylinderArea** = value from `machines.csv` for the selected machine.
correct
---

## Heater Plate Temperature

| Standard | Temperature Range |
|---|---|
| ISO 21307 SP Low Fusion | 225°C +/- 10 |
| ISO 21307 SP High Fusion | 215°C +/1 15 |
| DVS 2207 | 200°C – 220°C (ideal temperature varies, see table below) |

**DVS 2207 — Ideal (approximate) heater temperature:**

| Wall Thickness | Ideal Temp |
|---|---|
| < 3.5 mm | 220°C |
| 3.5 – 10 mm | 215°C |
| 10 – 15 mm | 210°C |
| 15 – 20 mm | 205°C |
| 20 – 40 mm | 203°C |
| > 40 mm | 200°C |

---

## Minimum Bead Size

| Standard | Formula |
|---|---|
| ISO 21307 SP Low Fusion | `ROUND(0.5 + 0.1 × wallThickness)`, maximum 6 mm |
| ISO 21307 SP High Fusion | `ROUND(1.0 + 0.15 × wallThickness)` |
| DVS 2207 | Same as ISO SP Low Fusion |

---

## Minimum Heat Soak Time

| Standard | Formula |
|---|---|
| ISO 21307 SP Low Fusion | `ROUND(wallThickness × 13.5)` seconds |
| ISO 21307 SP High Fusion | `ROUND(wallThickness × 11.0)` seconds |
| DVS 2207 | `ROUND(wallThickness × 10.0)` seconds |

> ⚠️ **Please verify:** Is 13.5 sec/mm correct for your ISO 21307 edition?

---

## Maximum Heater Plate Removal Time

*(Same table for ISO SP Low Fusion, High Fusion. DVS has a slightly shorter upper end.)*

| Wall Thickness (mm) | ISO LF & HF (sec) | DVS 2207 (sec) |
|---|---|---|
| ≤ 4.5 | 5 | 5 |
| 4.5 – 7.0 | 6 | 6 |
| 7.0 – 12.0 | 8 | 8 |
| 12.0 – 19.0 | 10 | 10 |
| 19.0 – 26.0 | 12 | 12 |
| 26.0 – 37.0 | 16 | 16 |
| 37.0 – 50.0 | 20 | 20 |
| 50.0 – 70.0 | 25 | *(not listed — 25 used)* |
| 70.0 – 90.0 | 30 | *(not listed — 30 used)* |
| > 90.0 | 35 | *(not listed — 35 used)* |

---

## Minimum Cooling Time

**ISO 21307 SP Low Fusion:**

```
If wallThickness < 18 mm:
    coolingTime = ROUND((wallThickness + 3) × 60)  seconds

If wallThickness ≥ 18 mm:
    coolingTime = ROUND((0.015 × wt² − 0.47 × wt + 20) × 60)  seconds
```

**ISO 21307 SP High Fusion:**

```
coolingTime = ROUND(wallThickness × 0.43 × 60)  seconds
```
*(No "Minimum Leave Time After Weld" for HF — shown as N/A)*

**DVS 2207 — Lookup table:**

| Wall Thickness (mm) | Min Cooling Time |
|---|---|
| < 4.5 | 6 min |
| 4.5 – 7 | 10 min |
| 7 – 12 | 16 min |
| 12 – 19 | 24 min |
| 19 – 26 | 32 min |
| 26 – 37 | 45 min |
| 37 – 50 | 60 min |
| > 50 | 80 min |

---

## Facing Pressure (max)

All standards:

```
maxFacingPressure = drag + 20    [Bar]
```

---

## DVS 2207 — Max Alignment Gap Width

| OD | Max Gap |
|---|---|
| < 355 mm | 0.5 mm |
| 355 – 630 mm | 1.0 mm |
| 630 – 800 mm | 1.3 mm |
| 800 – 1000 mm | 1.5 mm |
| > 1000 mm | 2.0 mm |

