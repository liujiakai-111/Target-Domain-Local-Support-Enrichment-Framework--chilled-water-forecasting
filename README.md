# Target Domain Local Support Enrichment for Chilled Water Load Forecasting

This repository contains the code and reproducible experiment workflow for target domain local support enrichment in office chilled water load forecasting with limited target data.

## Overview

The framework generates conditional residual trajectories from the observed target building, evaluates candidate utility using support data only, screens temporal compatibility within observed operating regimes, and uses selected synthetic windows during self supervised learning. Final supervised training uses real target labels only.

The repository supports:

- the main experiment on 30 office chilled water buildings;
- eight support lengths from 1 to 28 days;
- Branch A, Branch B, and Strategy C comparisons;
- module ablation experiments;
- candidate screening diagnostics;
- LBNL Building 59 and FRP exploratory cases;
- aggregation of results and generation of manuscript figures.

## Repository status

The code used for the manuscript is being reorganized into a reproducible structure. Raw datasets and large intermediate files are not distributed in this repository.

## Repository structure

- `src/tdlse/`: reusable implementation of the proposed framework;
- `configs/`: main, ablation, and external experiment settings;
- `scripts/`: data preparation, training, evaluation, and plotting entry points;
- `data/`: local data directories and data access instructions;
- `results/summary/`: compact numerical results used in the manuscript;
- `figures/`: scripts and final manuscript figures;
- `docs/`: experiment mapping and implementation notes.

## Environment

The original experiments used:

- Python 3.9.7
- NumPy 2.0.2
- pandas 2.2.3
- Matplotlib 3.9.4
- scikit-learn 1.6.0
- PyTorch 2.5.1 with CUDA 11.8

Install the required packages with:

```bash
pip install -r requirements.txt
