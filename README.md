# C.L.A.S.P — Classical Lamination Analytical Solver Program

A browser-based Classical Laminate Theory (CLT) solver for composite laminates. Single HTML file, zero dependencies, works fully offline.

**[Try it live →](https://toanle6543-max.github.io/CLASP/clasp.html)**

<img width="1523" height="845" alt="image" src="https://github.com/user-attachments/assets/ae922a00-6a28-44fb-99bd-2d41fb2ddca1" />
<img width="1864" height="740" alt="image" src="https://github.com/user-attachments/assets/d9334c9a-31ab-4b4c-9deb-dfc74f485253" />
<img width="1860" height="765" alt="image" src="https://github.com/user-attachments/assets/3c74dd5a-df22-4c41-96f9-9c2a16a86047" />


---

## Overview

C.L.A.S.P is a browser-based Classical Laminate Theory solver for composite laminates. Originating from a makeshift MATLAB tool built to solve homework problems, this program implements those fundamental mechanics and equations with a straightforward, user-friendly interface.

It computes the ABD stiffness matrix, ply-by-ply stresses and strains, and first-ply failure loads (Max Stress, Max Strain, and Hashin–Rotem criteria), with support for arbitrary layups, multiple materials, and both Imperial and Metric units. An iterative process can also determine the loading under which a layup fails, with per-component load scaling and constant holds.

The underlying math has been independently cross-checked against the original MATLAB implementation to 6 significant figures. See [Validation](#validation) below.

---

## Features

**Materials & layup**
- Add/remove any number of materials, each with full moduli, Poisson's ratio, CTE, thickness, and strength properties
- Arbitrary ply count, angle, and material assignment per ply
- Mirror Up / Mirror Down — build a symmetric layup from a half-stack in one click
- Live ply-stack schematic showing fiber orientation, material, and thickness to scale

**Analysis**
- **Direct Solve** — stresses, strains, and margins at a given load
- **Find Failure Load** — iterative search for the first-ply-failure load, with independent per-component scaling (e.g. scale Nx normally, Ny at half rate, hold Mx constant)
- Max Stress, Max Strain, and Hashin–Rotem (quadratic) failure criteria
- Thermal loading (ΔT), with equivalent thermal load/moment (NT, MT) reported explicitly

**Output**
- Full ABD stiffness matrix
- Ply-by-ply local stress/strain table (top and bottom of every ply)
- Through-thickness stress plot with unit-aware axes
- Critical ply cross-highlighted across the input list, stack view, and results table
- One-click PDF export of the full configuration and results

**Usability**
- Imperial ⇄ Metric unit conversion across every input and result
- Hoverable tooltips explaining every variable's physical meaning
- Reset button, input validation, and no page reloads — everything runs client-side

---

## Background

Classical Laminate Theory predicts how a stack of composite plies — each with its own fiber orientation and material — behaves as a single structural laminate under combined in-plane loads, bending moments, and thermal loading. The core result is the **ABD matrix**, which relates applied loads and moments to the laminate's midplane strain and curvature, and from there to the stress and strain state inside every individual ply. Hand-calculating this for anything beyond a few plies is slow and error-prone, which is the practical reason this tool exists.

---

## Validation

The JavaScript implementation was checked against the original MATLAB scripts by independently re-deriving the ABD matrix, midplane strain/curvature, and ply stresses for a fixed test case and comparing outputs directly.

| Quantity | MATLAB (exact) | C.L.A.S.P |
|---|---|---|
| A11 (lbf/in) | 463433.60 | 463434 |
| A22 (lbf/in) | 397362.85 | 397363 |
| B11 (lbf) | 980.71 | 980.711 |
| D11 (lbf·in) | 57.970 | 57.9701 |

All values agree to 6 significant figures. Thermal equivalent load/moment (NT, MT) were checked the same way against the original script's output.

---

## How to Use

No install, no build step, no server:

1. Download `clasp.html` (or open the [live version](https://toanle6543-max.github.io/CLASP/clasp.html))
2. Open it in any modern browser
3. Add a material → build a layup → enter loads → click **Run Analysis**

To use it offline, download and run the `.html` file.

---

## Tech Stack

- Plain HTML, CSS, and JavaScript. No frameworks, no build tools, no npm dependencies
- Single self-contained file by design, so it works fully offline and can be shared/run anywhere without setup
- PDF export uses the browser's native print-to-PDF rather than a bundled PDF library, for the same reason

---

## Known Limitations

- Assumes linear-elastic ply behavior (no progressive damage or post-first-ply-failure analysis)
- First-ply failure only — does not model final laminate failure after initial ply cracking
- Iterative failure-load search assumes the failure ratio increases monotonically with load magnitude

---

## Author

**Toan Le**
Structural Engineering, UC San Diego
[LinkedIn](https://www.linkedin.com/in/toan-minh-le/)

---

## License

MIT
