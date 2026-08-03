# Target Domain Local Support Enrichment for Chilled Water Load Forecasting

> **Code availability:** The complete implementation and reproducibility materials will be released in this repository after the associated manuscript is accepted for publication.

## Overview

This repository provides information about a target domain local support enrichment framework for office chilled water load forecasting with limited target data.

The method is designed for buildings with only a short operating history. It does not rely on source buildings and does not use synthetic labels during supervised model training.

The framework generates conditional residual trajectories from the observed target building. Generated candidates are evaluated through operational plausibility screening, forecast utility estimated from support data, temporal screening within observed operating regimes, and balanced sampling.

Selected synthetic windows are used only during self-supervised learning (SSL). Final supervised training uses real target labels only.

## Method Summary

The complete workflow contains five main stages:

1. **Chronological data splitting**

   Each building is divided into support, validation, and test periods in chronological order. The support period is varied from 1 to 28 days, while the validation and test periods remain fixed.

2. **Input window construction**

   Historical chilled water load, weather variables, and calendar variables are converted into sliding windows for one hour ahead forecasting.

3. **Conditional residual trajectory generation**

   Continuous residual trajectories are generated using weather and calendar context from the target building. The residuals are combined with paired real trajectories before sliding windows are extracted.

4. **Candidate screening and sampling**

   Generated candidates are evaluated using operational plausibility, forecast utility estimated from support data, temporal consistency within the same observed regime, and balanced sampling across trajectories and anchors.

5. **Forecasting and final evaluation**

   Three forecasting configurations are compared using the same LSTM backbone and the same real labeled support data during final supervised training.

## Forecasting Configurations

The experiments compare three configurations:

- **Branch A:** supervised learning using real labeled support data;
- **Branch B:** SSL using real support data, followed by supervised training using real labels;
- **Strategy C:** validation selected use of SSL with selected synthetic support, with fallback to Branch A when the synthetic option is invalid or does not improve validation performance.

Synthetic windows are not used as supervised labels in any configuration.

## Experimental Scope

The main experiment includes:

- 30 office buildings with chilled water measurements;
- eight support lengths: 1, 3, 5, 7, 10, 14, 21, and 28 days;
- one hour ahead load forecasting;
- Branch A, Branch B, and Strategy C comparisons;
- three random seeds;
- module ablation experiments;
- candidate screening diagnostics;
- site deletion sensitivity analysis;
- case level heterogeneity analysis.

Two related HVAC datasets are included as exploratory feasibility cases.

## Repository Status

This repository currently provides project information and describes the planned reproducibility package.

The complete source code, experiment configurations, data processing workflow, result aggregation scripts, and figure generation scripts are being organized. They will be released in this repository after the associated manuscript is accepted for publication.

Before the official release, this repository should not be considered a complete or executable implementation of the proposed method.

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

CUDA is not mandatory. A CPU installation of PyTorch can also be used, although model training will be slower.

## Installation

Installation and execution will be available after the official code release.

After release, the repository can be cloned using:

```bash
git clone https://github.com/liujiakai-111/target-domain-chilled-water-forecasting.git
cd target-domain-chilled-water-forecasting
```

Create a Python virtual environment:

```bash
python -m venv .venv
```

Activate the environment on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Activate the environment on Linux or macOS:

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

After downloading, raw data should be stored locally under:

```text
data/raw/
```

Processed feature files should be stored under:

```text
data/processed/
```

These directories are excluded from Git tracking.

## Reproduction

Detailed reproduction instructions will be released after the associated manuscript is accepted for publication.

The planned release will include commands for:

1. selecting and preparing the 30 target buildings;
2. constructing the engineered feature table;
3. running the main experiment at all eight support lengths;
4. running Branch A, Branch B, and Strategy C;
5. running the module ablation experiments;
6. running the exploratory external HVAC cases;
7. aggregating case and site results;
8. generating the manuscript figures.

Raw datasets will not be included in the repository. Users will need to obtain them from the original sources.

## Results

Compact numerical summaries used in the manuscript will be released under:

```text
results/summary/
```

Large per-run outputs, model checkpoints, temporary candidate pools, and processed datasets will not be uploaded.

The released summaries will contain the information needed to reproduce the reported tables and figures without redistributing restricted raw data.

## Citation

The associated manuscript is currently under review.

If you are interested in this work, please follow this repository for future updates. The complete journal citation, DOI, and BibTeX entry will be added after the manuscript is accepted and published.

Preliminary manuscript information:

```text
Liu, J., and Chen, Y. Target Domain Local Support Enrichment through
Utility Screening of Conditional Residual Trajectories for Office
Chilled Water Load Forecasting with Limited Target Data.
Manuscript under review.
```

## License

The source code will be released under the [MIT License](LICENSE).

The MIT License applies only to the source code in this repository. Dataset licenses, copyrights, and terms of use remain with the original data providers.

## Contact

**Jiakai Liu**  
School of Energy and Power Engineering  
University of Shanghai for Science and Technology  
Shanghai 200093, China  

Email: [1602252955@qq.com](mailto:1602252955@qq.com)

## Contact

**Jiakai Liu**  
School of Energy and Power Engineering  
University of Shanghai for Science and Technology  
Shanghai 200093, China
