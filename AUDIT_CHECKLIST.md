# Audit Checklist for Weldpoly Engineers

Please review each item and update the relevant file, or leave a comment in the **Issues** tab.

---

## machines.csv — Machine Data

- [ ] **Cylinder Area (mm²)** — Verify each machine's cylinder area against hydraulic cylinder spec sheets.  
  This is the **only machine-specific input** — all pressure calculations are derived from it.

- [ ] **Max OD (mm)** — Confirm the maximum pipe OD listed for each machine matches actual machine capacity.

- [ ] **Min OD (mm)** — Currently 40 mm for all machines. Is this correct?

- [ ] **Welding Standard** — Confirm the correct standard (LF / HF / DVS) is assigned to each machine.

- [ ] **Any machines missing?** — Are there machines that should be added to the app?

---

## FORMULAS.md — Calculation Formulas

- [ ] **Interfacial pressure constant (ISO SP Low Fusion)** — Currently **0.17 MPa**. Correct?

- [ ] **Interfacial pressure constant (ISO SP High Fusion)** — Currently **0.52 MPa**. Correct?

- [ ] **Heat soak multiplier (ISO LF)** — Currently **13.5 sec/mm**. Correct per your ISO 21307 edition?

- [ ] **Heat soak multiplier (ISO HF)** — Currently **11.0 sec/mm**. Correct?

- [ ] **Heat soak multiplier (DVS)** — Currently **10.0 sec/mm**. Correct?

- [ ] **Cooling time formula (ISO LF)** — Quadratic formula for wall ≥ 18mm. Verify against ISO 21307 Annex A.

- [ ] **Cooling time table (DVS)** — Verify all values against current DVS 2207-1 edition.

- [ ] **Max heater removal time table** — Verify all values against standard tables.

- [ ] **Minimum bead size formulas** — Verify coefficients for LF and HF.

- [ ] **DVS gap width values** — Verify all values against DVS 2207-1.

---

## How to propose a change

1. Open the file you want to edit (`machines.csv` or `FORMULAS.md`)
2. Click the **pencil icon ✏️** (top right of the file view)
3. Make your changes
4. Scroll down → **"Propose changes"** → **"Create pull request"**
5. Add a short description of what you changed and why

> Alternatively, open an **Issue** (tab at the top of this page) to describe a problem without editing the file directly.
