# Target Domain Local Support Enrichment for Chilled Water Load Forecasting

This repository contains the code, experiment configurations, and reproducibility workflow for target domain local support enrichment in office chilled water load forecasting with limited target data.

## Overview

Accurate chilled water load forecasting is difficult when a target building has only a short operating history. This project addresses that problem without transferring knowledge from source buildings or using synthetic labels during supervised training.

The proposed framework generates conditional residual trajectories from the observed target building. Generated candidates are evaluated using operational plausibility, forecast utility estimated from support data, temporal consistency within observed operating regimes, and balanced sampling.

Selected synthetic windows are used only during self-supervised learning (SSL). Final supervised training uses real target labels only.

The framework compares three forecasting configurations:

- **Branch A:** supervised learning using real labeled support data;
- **Branch B:** SSL using real support data, followed by supervised training using real labels;
- **Strategy C:** validation selected use of SSL with synthetic support, with fallback to Branch A when the synthetic option is invalid or does not improve validation performance.

## Main Features

- Target building data are used without relying on source buildings.
- Continuous residual trajectories are generated before sliding window extraction.
- Weather and calendar variables provide operating context.
- Synthetic candidates are screened using support data only.
- Synthetic windows are used only during SSL.
- Supervised training uses real target labels only.
- Validation selects the synthetic ratio and controls fallback.
- Main experiments, ablations, external cases, and figure generation are included in the planned release.

## Experimental Scope

The main experiment contains:

- 30 office buildings with chilled water measurements;
- eight support lengths: 1, 3, 5, 7, 10, 14, 21, and 28 days;
- one hour ahead load forecasting;
- Branch A, Branch B, and Strategy C comparisons;
- three random seeds;
- module ablation studies;
- candidate screening diagnostics;
- site deletion sensitivity analysis;
- case level heterogeneity analysis.

Two additional HVAC datasets are used as exploratory feasibility cases.

## Repository Status

The code used for the manuscript is currently being reorganized into a clear and reproducible structure.

Raw datasets, model checkpoints, and large intermediate files are not distributed in this repository. Reproduction commands will be added after the experiment scripts and configurations have been checked and organized.

## Planned Repository Structure

```text
target-domain-chilled-water-forecasting/
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── .gitignore
├── configs/
│   ├── main_experiment.json
│   ├── ablations/
│   └── external_cases/
├── src/
│   └── tdlse/
│       ├── __init__.py
│       ├── data.py
│       ├── features.py
│       ├── residual_generation.py
│       ├── screening.py
│       ├── ssl.py
│       ├── forecasting.py
│       └── metrics.py
├── scripts/
│   ├── prepare_target_cases.py
│   ├── build_features.py
│   ├── run_main_experiment.py
│   ├── run_ablations.py
│   ├── run_external_cases.py
│   ├── aggregate_results.py
│   └── make_figures.py
├── data/
│   ├── README.md
│   ├── raw/
│   ├── interim/
│   └── processed/
├── results/
│   ├── README.md
│   └── summary/
├── figures/
├── docs/
│   └── experiment_mapping.md
└── tests/
```

## Environment

The original experiments were conducted with:

- Python 3.9.7
- NumPy 2.0.2
- pandas 2.2.3
- Matplotlib 3.9.4
- scikit-learn 1.6.0
- PyTorch 2.5.1
- CUDA 11.8

The CUDA version is not mandatory. A CPU installation of PyTorch can also be used, although model training will be slower.

## Installation

Clone the repository:

```bash
git clone https://github.com/liujiakai-111/target-domain-chilled-water-forecasting.git
cd target-domain-chilled-water-forecasting
```

Create a Python virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Activate it on Linux or macOS:

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

## Data

The main experiment uses office chilled water data from the Building Data Genome Project 2 (BDG2).

The exploratory cases use the following datasets:

- [LBNL Building 59](https://bbd.labworks.org/ds/bbd/lbnlbldg59)
- [ORNL Flexible Research Platform data via the TUM EMT Open Energy Data Collection](https://collab.dvb.bayern/spaces/TUMenmantech/pages/557810667/TUM-EMT+Open+Energy+Data+Collection)

Raw data are not redistributed in this repository. Users should obtain the datasets from their original sources and comply with the corresponding licenses and terms of use.

Downloaded files should be stored locally under:

```text
data/raw/
```

Processed feature files should be stored under:

```text
data/processed/
```

Both directories are excluded from Git tracking.

## Reproduction

The organized release will provide commands for:

1. selecting and preparing the 30 target buildings;
2. constructing the engineered feature table;
3. running the main experiment at all eight support lengths;
4. running Branch A, Branch B, and Strategy C;
5. running the module ablation experiments;
6. running the external HVAC cases;
7. aggregating case and site results;
8. generating the manuscript figures.

Detailed commands will be added after the corresponding scripts and configurations have been verified.

## Results

Compact numerical summaries used in the manuscript will be stored in:

```text
results/summary/
```

Large per-run outputs, model checkpoints, temporary candidate pools, and processed datasets are excluded from the repository.

The committed summaries should contain enough information to reproduce the reported tables and figures without publishing restricted raw data.

## Citation

If you use this repository, please cite the associated manuscript:

```text
Liu, J., and Chen, Y. Target Domain Local Support Enrichment through
Utility Screening of Conditional Residual Trajectories for Office
Chilled Water Load Forecasting with Limited Target Data.
Manuscript under review.
```

The complete journal citation and DOI will be added after publication.

## License

The source code is released under the [MIT License](LICENSE).

The MIT License applies only to the code in this repository. Dataset licenses, copyrights, and terms of use remain with the original data providers.

## Contact

**Jiakai Liu**  
School of Energy and Power Engineering  
University of Shanghai for Science and Technology  
Shanghai 200093, China
