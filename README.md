# imwa-workshop-2026

<p align="center">
  <img src="asset/imwa2026.png" alt="IMWA 2026" width="400">
</p>

[![CI](https://github.com/p-ortega/imwa-workshop-2026/actions/workflows/ci.yml/badge.svg)](https://github.com/p-ortega/imwa-workshop-2026/actions/workflows/ci.yml)

Workshop tutorials for the International Mining Water Association Conference in Korea, 2026.

## Overview

An end-to-end groundwater decision-support workflow for an open-cut mine facing acid
mine drainage (AMD) impacts on groundwater. The tutorials walk through the full chain:
MODFLOW 6 flow modelling → conservative transport → reactive transport (mf6rtm / PHREEQC)
→ PEST/PEST++ parameter estimation → ensemble uncertainty quantification (PESTPP-IES)
→ constrained decision optimization (PESTPP-OPT).

## Prerequisites

- `git`
- A conda distribution — `conda`, `mamba`, or `micromamba`. [Miniforge](https://github.com/conda-forge/miniforge#install) is recommended (ships `conda` + `mamba`, defaults to the conda-forge channel). Alternatives: [Miniconda](https://www.anaconda.com/download/success) or [micromamba](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html).
- A few GB of free disk space (bundled dependencies + solver/PEST binaries)

## Installation

Everything needed ships in the repo: FloPy / pyEMU / mf6rtm libraries are 
under `dependencies/` and installed editable, and the MODFLOW 6 and PEST++ binaries are
committed under `tutorial/bin/`. A plain clone plus one conda command is all it takes.

```bash
git clone https://github.com/p-ortega/imwa-workshop-2026.git
cd imwa-workshop-2026
conda env create -f environment.yml   # creates env "imwa2026" (mamba/micromamba also work)
conda activate imwa2026
```

**Linux / macOS** — make the bundled binaries executable:

```bash
chmod +x tutorial/bin/linux/* tutorial/bin/mac/*
```

## Running the tutorials

```bash
jupyter lab      # or: jupyter notebook
```

Open the `tutorial/` folder and run the notebooks **in numeric order** — each one reuses
outputs produced by the previous one.

## Tutorials

| Notebook | Topic |
|---|---|
| `00-dewatering-flow` | MODFLOW 6 transient flow for an open-cut mine: pit dewatering wells, managed aquifer recharge (MAR), and a groundwater-dependent ecosystem (GDE) drain. |
| `01-conservative-transport` | Adds a GWT model for the conservative AMD tracer plume from the tailings facility (advection/dispersion, GWF–GWT coupling). |
| `02-reactive-transport` | Couples MODFLOW 6 with PHREEQC via mf6rtm: AMD chemistry, calcite buffering, and GDE pH evolution. |
| `03-pstfrom` | Uses pyEMU `PstFrom` to build a highly parameterized PEST setup (flow, transport, and chemistry parameters). |
| `04-priomc` | Prior Monte Carlo ensemble with PESTPP-IES — pre-calibration forecast uncertainty. |
| `05-ies` | PESTPP-IES history matching against heads, GDE flux, pH, and well chemistry; observation weighting, noise, and localization. |
| `06-opt` | PESTPP-OPT decision optimization under uncertainty: chance constraints, a pH constraint, and MAR treatment as a decision variable. |
