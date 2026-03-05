# sr-trbm
Self-Regulated Thermodynamic RBM: Controlled non-equilibrium training with endogenous temperature dynamics.

[![arXiv](https://img.shields.io/badge/arXiv-2603.02525-b31b1b.svg)](https://arxiv.org/abs/2603.02525)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18778493.svg)](https://doi.org/10.5281/zenodo.18778493)

![PyTorch](https://img.shields.io/badge/PyTorch-2.x-ee4c2c.svg)
![Python](https://img.shields.io/badge/python-3.10-blue)

Hybrid Thermodynamic Restricted Boltzmann Machine with endogenous micro–macro temperature regulation and AIS-based partition estimation.

- Note: In the code implementations, the bias decay has been set to 0.

Overview

This repository implements the Self-Regulated Thermodynamic Restricted Boltzmann Machine (SR-TRBM) introduced in:

Görkem Can Süleymanoğlu (2026).
Controlled Thermal Non-Equilibrium Training of Restricted Boltzmann Machines.

The proposed model tackles a structural instability mechanism inherent to fixed-temperature, finite-time Contrastive Divergence training. When effective fields diverge under a fixed sampling temperature, Gibbs transition probabilities decay, conductance collapses, and the negative phase localizes, potentially inducing linear parameter drift.

SR-TRBM addresses this structural instability by introducing:

* Endogenous temperature dynamics
* Micro-level flip-rate feedback regulation
* Macro-level Cesàro-averaged free-energy stabilization
* AIS-based partition estimation

The temperature is treated as a dynamical state variable rather than as a fixed hyperparameter.

---

Core Features

* Endogenous micro–macro temperature control
* Adaptive flip-rate feedback regulation
* Persistent Contrastive Divergence (PCD-K, K is a natural number.)
* Annealed Importance Sampling (AIS)
* Effective inverse temperature diagnostics
* Full thermodynamic trajectory monitoring

---

Model Configuration (Paper Setting)

* Visible units: 784
* Hidden units: 512
* Training epochs: 400
* Gibbs steps: 1
* Batch size: 128
* Learning rate: 5e-4
* Weight decay: 1e-4

---

Installation

Recommended environment:

* Ubuntu 22.04 LTS
* CUDA 12.x
* PyTorch 2.x

Install dependencies:

pip install -r requirements.txt

---

Running Experiments

Adaptive regime:

python srtrbm_project0.py --temperature adaptive, fixed_temperature=None

Fixed temperature baseline:

python srtrbm_project0.py --temperature fixed, fixed_temperature=1.0

Frozen tuned temperature:

python srtrbm_project0.py --temperature frozen fixed_temperature=X, any real number

Each seed runs independently. Multi-GPU execution is supported in PyTorch via explicit CUDA device binding.

---

Output

Each run reports:

* Final temperature trajectory
* Effective inverse temperature (β)
* Train & test log-likelihood
* Reconstruction MSE
* AIS log-partition estimate
* AIS Effective Sample Size (ESS)
* Created samples
* Thermodynamic diagnostics

---

Reproducibility

For deterministic reproduction:

* Fix random seeds
* Use identical CUDA and driver versions
* Run one seed per GPU
* Avoid GPU oversubscription

All experiments reported in the paper can be reproduced using the configuration provided in this repository.

---

Citation

If you use this implementation, please cite:

Paper (arXiv):
Süleymanoğlu, G. C. (2026). Thermodynamic regulation of finite-time Gibbs training in energy-based models: A restricted Boltzmann machine study. arXiv. https://arxiv.org/abs/2603.02525

Software (Zenodo):
Süleymanoğlu, G. C. (2026). Self-Regulated Thermodynamic RBM (SR-TRBM) [Software]. Zenodo. https://doi.org/10.5281/zenodo.18778493

---

License

BSD 3-Clause License
Copyright (c) 2026 Görkem Can Süleymanoğlu
