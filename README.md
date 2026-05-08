# Nuclear Fission Chain Reaction — Monte Carlo Simulation

A Python simulation of nuclear fission chain reactions using Monte Carlo methods. The project models neutron population dynamics across generations and compares simulated outcomes against theoretical predictions from branching process theory.

---

## Overview

Each neutron has a fixed probability `p` of striking a U-235 nucleus and causing fission. A fission event releases `n_fission` new neutrons, which go on to trigger further reactions. The key parameter is the **effective neutron multiplication factor**:

$$k_{\text{eff}} = p \times n_{\text{fission}}$$

- $k_{\text{eff}} < 1$ — subcritical: reaction dies out
- $k_{\text{eff}} = 1$ — critical: reaction sustains
- $k_{\text{eff}} > 1$ — supercritical: reaction grows exponentially

The theoretical expected population at generation $g$ is $k_{\text{eff}}^g$, derived from branching process theory. The simulation runs many independent chains and averages them, demonstrating convergence to this theoretical value.

---

## Project Structure

```
fission_chain_phase1.ipynb   # Main notebook
fission_note.svg             # Fission illustration (embedded in notebook)
README.md
```

---

## Notebook Contents

- **Parameters** — `p`, `n_fission`, `n_gen`, `n_trials`, `seed`
- **`simulate_chain()`** — Monte Carlo simulation of one fission chain
- **`run_trials()`** — ensemble of independent chains returning a `(n_trials, G+1)` array
- **`theoretical_curve()`** — closed-form branching process expectation $k_{\text{eff}}^g$
- **Comparison table** — simulated mean vs theoretical, with absolute and relative error
- **Plots** — simulated vs theoretical on linear and log scales, all three regimes side by side, and relative error per generation

---

## Requirements

```
numpy
matplotlib
pandas
```

Install with:

```bash
pip install numpy matplotlib pandas
```

Or run the first cell in the notebook which handles installation automatically.

---

## Roadmap

**Phase 2 — Spatial model**
Assign each neutron a position $(r, \theta, \phi)$ in a spherical reactor. Replace fixed `p` with a spatially-varying $p(r)$ based on the neutron diffusion flux profile:

$$\phi(r) \propto \frac{\sin(\pi r / R)}{r}$$

Neutrons near the surface have a higher escape probability and therefore a lower effective `p`.

**Phase 3 — Future work**
Model time-varying $p(r, t)$ as fissile material depletes, leading into the neutron transport and diffusion PDE:

$$\frac{1}{v}\frac{\partial \phi}{\partial t} = D\nabla^2\phi - \Sigma_a \phi + S$$

Numerical PDE methods (finite difference, finite element) would be required at this stage.

---

## References

- Galton-Watson branching process theory
- Lamarsh, *Introduction to Nuclear Reactor Theory*
- Duderstadt & Hamilton, *Nuclear Reactor Analysis*

