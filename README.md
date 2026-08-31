# Transfer Learning for Building Energy Prediction

This repository contains the implementation code and data processing pipelines for our paper:

**"A Dynamic Time Warping-Enhanced Transfer Learning Framework for Cooling Load Prediction in Data-Scarce Buildings: A Multi-Building Case Study"**

## Current Status

**Note**: The complete source code is currently being prepared for public release and will be made available upon the final acceptance of the manuscript. This repository is established in accordance with reproducibility and open science guidelines.

**Expected release timeline**: Within 2 weeks after manuscript acceptance.

## Paper Information

- **Title**: A Dynamic Time Warping-Enhanced Transfer Learning Framework for Cooling Load Prediction in Data-Scarce Buildings: A Multi-Building Case Study
- **Authors**: Jiakai Liu, Yongbao Chen*, Zhe Chen
- **Affiliations**: 
  - School of Energy and Power Engineering, University of Shanghai for Science and Technology, Shanghai, China
  - Department of Building Environment and Energy Engineering, The Hong Kong Polytechnic University, Hong Kong, China
- **Corresponding Author**: Yongbao Chen (chenyongbao@usst.edu.cn)
- **Repository URL**: https://github.com/liujiakai-111/Transfer-Learning-building-energy

## Research Overview

This study addresses building cooling load prediction under data-scarce conditions by developing a novel transfer learning framework. The key contributions include:

1. **Source building selection optimization**: A multi-dimensional Dynamic Time Warping (DTW) similarity measurement method
2. **Multi-feature integration**: Weighted similarity analysis incorporating both cooling load and meteorological parameters
3. **Comprehensive model development**: Five prediction models including baseline and transfer learning variants
4. **Empirical validation**: Real office building data from five different climate zones

## Methodology

### Data Preprocessing
- Data cleaning: outlier removal, missing value imputation, weekend data filtering
- Feature engineering: 
  - Temporal features (sinusoidal encoding of hour and day)
  - Lag features (1, 2, 3, 24, 48-hour lags)
  - Statistical features (3-hour and 24-hour moving averages)
  - Cross-features (temperature-to-humidity ratio)
  - Meteorological parameters and occupancy schedule

### Multi-dimensional DTW Similarity
- Weighted Euclidean distance based on feature importance
- Features considered: cooling load, air temperature, dew point temperature
- Source building selection: Top 3 most similar buildings

### Prediction Models
Five models were implemented and compared:

| Model Type | Model Name | Description |
|------------|------------|-------------|
| Baseline | LightGBM | Gradient boosting baseline |
| Baseline | LSTM | Long Short-Term Memory baseline |
| Transfer Learning | LightGBM-WI | LightGBM with weight initialization |
| Transfer Learning | LSTM-FT | LSTM with fine-tuning |
| Transfer Learning | LSTM-FE | LSTM with feature extraction |

## Data Source

This study utilizes the **Building Data Genome Project 2 (BDGP2)** dataset:

- Dataset URL: https://www.kaggle.com/datasets/claytonmiller/buildingdatagenomeproject2
- Citation: Miller, C. et al. The Building Data Genome Project 2, energy meter data from the ASHRAE Great Energy Predictor III competition. Sci Data 7, 368 (2020).
- Time period: 2016-2017 (hourly data)
- Building selection: 5 target office buildings and 25 source office buildings
- Climate zones: Desert, Humid subtropical, Humid continental

## Expected Repository Structure

Transfer-Learning-building-energy/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│ ├── raw/ # Original BDGP2 data
│ ├── processed/ # Preprocessed data
│ └── sample/ # Sample data for testing
├── scripts/
│ ├── data_preprocessing.py
│ ├── dtw_similarity.py
│ └── feature_engineering.py
├── models/
│ ├── lightgbm_models.py
│ ├── lstm_models.py
│ └── transfer_strategies.py
├── config/
│ └── hyperparameters.yaml
├── utils/
│ ├── metrics.py
│ └── visualization.py
└── results/ # Output directory

## Technical Requirements

- Python 3.8+
- Key Python libraries: pandas, numpy, scikit-learn, lightgbm, torch/tensorflow, fastdtw, matplotlib

## Key Results

Based on our experimental evaluation:

1. Transfer learning effectiveness:
   - LightGBM-WI: 15.75% average reduction in CVRMSE compared to baseline
   - LSTM-FT: 13.19% average reduction in CVRMSE compared to baseline

2. Source selection importance:
   - DTW-based screening further reduced prediction error by 1.62% (LightGBM-WI) and 13.65% (LSTM-FT) compared to using all source buildings

3. Model comparison insights:
   - LSTM generally outperformed LightGBM in baseline comparisons
   - Fine-tuning was more effective than feature extraction for LSTM models
   - LightGBM-WI offered better stability while LSTM-FT achieved higher accuracy peaks

## Usage Instructions

Once released, users can reproduce our experiments with the following steps:

```bash
# Install dependencies
pip install -r requirements.txt

# Run data preprocessing
python scripts/data_preprocessing.py

# Calculate building similarities
python scripts/dtw_similarity.py

# Train and evaluate models
python models/lightgbm_models.py
python models/lstm_models.py
```
## Citation
If you use this work in your research, please cite:
@article{liu2025dtwtransfer,
  title={A Dynamic Time Warping-Enhanced Transfer Learning Framework for Cooling Load Prediction in Data-Scarce Buildings: A Multi-Building Case Study},
  author={Liu, Jiakai and Chen, Yongbao and Chen, Zhe},
  journal={Submitted for publication},
  year={2025}
}

## Contact
For questions about the paper: Yongbao Chen (chenyongbao@usst.edu.cn)
For questions about the code: Jiakai Liu (1602252955@qq.com)
Repository updates will be provided upon manuscript acceptance

## Reproducibility Commitment
We are committed to open science and will provide:
1.Complete implementation of all experiments described in the paper
2.Detailed documentation and step-by-step instructions
3.Example data and configuration files
4.Full reproducibility guide

