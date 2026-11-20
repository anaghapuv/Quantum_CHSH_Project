# CHSH Violations using Dynamic Circuits

Simulation of **Waring, Pere & Le Beux (2025)**, *"CHSH Violations using Dynamic Circuits"* ([arXiv:2504.18429](https://arxiv.org/abs/2504.18429)), implemented in Qiskit.

## Overview

This project investigates how well Bell-pair entanglement survives across a linear chain of `d` qubits (`d = 2..8`) under realistic hardware noise, by measuring the CHSH score:

$$S(\phi) = \langle ZZ\rangle_\phi - \langle ZX\rangle_\phi + \langle XZ\rangle_\phi + \langle XX\rangle_\phi$$

- **Classical limit:** $|S| \le 2$
- **Quantum (Tsirelson) limit:** $|S| \le 2\sqrt{2} \approx 2.83$

Three entanglement distribution methods are compared on Qiskit's `AerSimulator` using the `FakeQuebec` noise model (a software model of IBM's 127-qubit `ibm_quebec` processor):

1. **Unitary (SWAP-based):** Moves qubit 0 down the chain using SWAP gates, applies a CNOT, and SWAPs back.
2. **Dynamic (Mid-circuit Measurements + Feedforward):** Entangles the chain, measures the intermediate qubits, and applies a conditional Z correction on the final qubit.
3. **Post-Processing:** Uses the same circuit as the Dynamic method without the feedforward Z correction, keeping only the shots where no correction was required.

## Notebook Contents

- **Setup & CHSH Helpers** — Configures `AerSimulator` with `FakeQuebec` noise (`2048` shots, `21` values of $\phi \in [-\pi/2, 3\pi]$, distances `2` through `8`).
- **Circuit Implementations** — Builders for the Unitary, Dynamic, and Post-Processing methods.
- **Simulation & Results** — Plots $\max|S|$ vs. qubit distance and $S(\phi)$ curves at $d = 3$ and $d = 6$.
- **Extension 1:** Transpiled 2-qubit gate count and circuit depth comparison.
- **Extension 2:** Effect of classical feed-forward delay on CHSH violation.
- **CHSH Concept Animation:** Interactive `matplotlib` animation illustrating Bell-pair distribution, basis selection, measurement shots, and CHSH score evaluation.

## Getting Started

### Run in Google Colab
Open `project_chsh.ipynb` in Google Colab and run the cells sequentially. The notebook installs the required packages automatically:

```bash
pip install qiskit qiskit-aer qiskit-ibm-runtime matplotlib numpy
```

> **Note:** The first cell mounts Google Drive (`drive.mount('/content/drive')`); you can skip or remove it if running locally.

### Run Locally
1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   cd <your-repo>
   ```
2. Install dependencies:
   ```bash
   pip install qiskit qiskit-aer qiskit-ibm-runtime matplotlib numpy jupyter
   ```
3. Launch Jupyter and open `project_chsh.ipynb`:
   ```bash
   jupyter notebook project_chsh.ipynb
   ```

## Reference

- Waring, Pere, & Le Beux (2025). *CHSH Violations using Dynamic Circuits*. [arXiv:2504.18429](https://arxiv.org/abs/2504.18429).
