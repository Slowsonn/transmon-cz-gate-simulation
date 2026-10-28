# transmon-cz-gate-simulation

Simulation code accompanying my M.Sc. thesis (Aalto University, Engineering Physics, Quantum Technology): a closed-system study of flux-pulsed CZ gates between two transmon qubits. Link to the thesis: https://aaltodoc.aalto.fi/items/763be234-354b-44dc-a2a0-cbc5dbd53075

## What this does

The code simulates a CZ gate between a flux-tunable and a fixed transmon, driven by a flux pulse that brings the |11⟩ and |20⟩ states through an avoided crossing. Four pulse shapes are compared (unipolar, net-zero bipolar, Gaussian-filtered bipolar, and adiabatic). For each pulse, the code optimizes the pulse parameters and reports average gate fidelity, leakage, and the |01⟩↔|10⟩ exchange error. A CNOT is built from each CZ by wrapping it in Hadamard gates on the target qubit, with the Hadamards implemented as DRAG pulses.

**Main findings**
- The average gate fidelity of every pulse is mainly limited by the exchange error, not just by leakage. This error is hidden from the usual |11⟩ population check.
- Net-zero pulses cancel the first-order phase on neighboring qubits but do not by themselves suppress the exchange error. The strong suppression of the analytic bipolar gate (0.013%) depends on its idle time, not on being net-zero.

## Contents

| Notebook | Description |
|---|---|
| `unipolar_cz.ipynb` | Unipolar flux pulse: parameter optimization, population dynamics, fidelity, exchange error |
| `bipolar_netzero_cz.ipynb` | Analytic net-zero bipolar pulse |
| `bipolar_gaussian_cz.ipynb` | Gaussian-filtered bipolar pulse |
| `adiabatic_cz.ipynb` | Adiabatic pulse (reference case) |
| `drag.ipynb` | DRAG implementation that is later used for CNOT |
| `pulses_comparison.ipynb` | Side-by-side comparison of the four pulse shapes |

Each notebook is self-contained and runs top to bottom. Outputs are saved, so results and plots are visible without running anything.

## Setup

```bash
pip install -r requirements.txt
```

The code uses [scqubits](https://github.com/scqubits/scqubits) for the exact diagonalization of the transmon Hamiltonian and [QuTiP](https://qutip.org/) for time evolution.

## Scope

This is a closed-system simulation. It does not include decoherence, so the reported fidelities describe the coherent error of each pulse, not the total infidelity of a physical device. Leakage is reported separately from the fidelity. Two parameter sets are used: a generic transmon set and one matched to a real device.

Hardware measurement notebooks are not included.

## License

MIT, see `LICENSE`.

## Author

Göktuğ Yavaşoğlu, M.Sc. Engineering Physics, Aalto University
