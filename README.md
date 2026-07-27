# AI-Surrogate Structural Optimization Pipeline

An end-to-end computational pipeline that leverages **Latin Hypercube Sampling (LHS)**, **Kriging (Gaussian Process Regression)**, and **SciPy's SLSQP algorithm** to optimize structural designs under mechanical safety constraints while minimizing computational overhead.

---

## Overview

High-fidelity numerical simulations (such as Finite Element Analysis) are computationally expensive when performing iterative structural optimization. This project builds a machine-learning surrogate model to approximate the physical design space, enabling real-time gradient-based optimization to minimize structural mass while maintaining deflection safety limits.

---

## Architecture & Workflow

1. **Design of Experiments (DoE):** Space-filling Latin Hypercube Sampling (LHS) generates a representative dataset across design parameters (Length $L$, Thickness $t$, and Load $W$).
2. **Physics Engine:** Ground-truth structural deflection data evaluated via Euler-Bernoulli beam mechanics.
3. **Surrogate Modeling:** Kriging model (Gaussian Process Regression) trained using the `smt` library to learn the non-linear response surface of deflection.
4. **Constrained Optimization:** Sequential Least Squares Programming (`SLSQP` via `scipy.optimize`) minimizes structural volume under two inequality constraints:
   - Maximum deflection rule: $\delta \leq 0.05\text{ m}$
   - Physical reality boundary: $\delta \ge 0.0\text{ m}$
5. **Visualization:** 3D surface mapping of the design space using `matplotlib`.

---

## Technical Stack

- **Language:** Python 3.x
- **Scientific Computing:** `NumPy`, `SciPy`
- **Surrogate Modeling:** `smt` (Surrogate Modeling Toolbox)
- **Visualization:** `Matplotlib`

---

## Results

- **Objective:** Minimize Beam Volume ($V = L \times b \times t$)
- **Optimal Length ($L$):** $1.000\text{ m}$
- **Optimal Thickness ($t$):** $0.0100\text{ m}$
- **Predicted Deflection:** $0.0012\text{ m}$ (Safely within the $0.05\text{ m}$ allowance)
<img width="811" height="659" alt="plot" src="https://github.com/user-attachments/assets/b5bd75b1-ebe1-4517-b3db-6a72092a7e81" />

---

## Roadmap / Phase 2 Integration

- **FEA Simulator Bridge:** Replacing analytical physics equations with automated batch runs from **SimScale (3D FEA)**.
- **Multi-Environment Optimization:** Integrating the **MATLAB Engine API for Python** to run benchmark comparisons using MATLAB's `fmincon` and `lhsdesign`.

