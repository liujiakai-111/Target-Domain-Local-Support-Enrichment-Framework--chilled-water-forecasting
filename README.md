# Target Domain Enhancement for Cooling Load Forecasting with Limited Data

This repository supports the manuscript:

**“Building cooling load forecasting with limited data: A few-shot target domain enhancement (TDE) framework”**

## Current status

The complete source code and processing pipeline are being organized for public release. They will be uploaded to this repository after the manuscript is formally accepted, with the release planned within two weeks of acceptance.

Until then, this README records the study design, data sources, expected repository structure, and reproducibility plan. The results reported here correspond to the submitted manuscript.

## Paper information

- **Authors:** Jiakai Liu, Yongbao Chen*, Jiahang Luo, and Zhe Chen
- **Affiliations:**
  - School of Energy and Power Engineering, University of Shanghai for Science and Technology, Shanghai, China
  - Department of Building Environment and Energy Engineering, The Hong Kong Polytechnic University, Hong Kong, China
- **Corresponding author:** Yongbao Chen (`chenyongbao@usst.edu.cn`)
- **Repository:** <https://github.com/liujiakai-111/Target-Domain-Local-Support-Enrichment-Framework--chilled-water-forecasting>

## Research overview

Cooling load forecasting models often have to be developed from only a few days of measurements. Transfer learning can reduce this data requirement, but it depends on suitable source buildings and may transfer irrelevant patterns when the source and target buildings differ.

The proposed target domain enhancement (TDE) framework uses only data from the target building. It generates controlled residual variations from local weather, calendar information, and measured load patterns. Generated samples are screened using the target training data, and useful samples are retained for self-supervised learning (SSL) pretraining. The forecasting model is then fine-tuned using measured target-building labels. Synthetic load values are not used as one-step-ahead forecasting labels.

## Framework

The workflow contains five main stages:

1. **Target data split and preprocessing**  
   Each building is divided chronologically into target training, validation, and test periods. Normalization is fitted only on the target training data.

2. **Input window construction**  
   Measured loads, local weather, and calendar variables are converted into sliding windows for one-hour-ahead forecasting.

3. **Residual trajectory generation**  
   A conditional generator produces continuous residual variations using weather and calendar information. These residuals are added to measured load trajectories to create new samples that remain consistent with the observed patterns.

4. **Candidate screening and selection**  
   Plausibility screening, forecasting utility checks, operating-regime checks, scoring, and balanced sampling determine which synthetic windows are retained. Candidate evaluation uses only the target training data and its inner folds.

5. **SSL pretraining and forecasting**  
   Selected synthetic windows are used with measured windows during SSL pretraining. Supervised fine-tuning uses measured target-training windows and measured one-step-ahead labels. Validation determines whether TDE is retained; otherwise, the traditional LSTM result is used. Test data are used only for final evaluation.

## Experimental design

The main experiment includes:

- 30 office buildings from six weather station sites;
- eight target-training lengths: 1, 3, 5, 7, 10, 14, 21, and 28 days;
- 240 building and support-length combinations;
- a fixed one-hour prediction horizon;
- the same LSTM architecture, features, data split, and supervised loss for all forecasting strategies;
- three random seeds for each configuration;
- module-level ablations, candidate diagnostics, and site sensitivity analysis.

The three forecasting strategies are:

- **Strategy A:** traditional supervised LSTM;
- **Strategy B:** SSL pretraining with measured target-training windows, followed by supervised fine-tuning;
- **Strategy C:** SSL pretraining with measured and selected synthetic windows, followed by supervised fine-tuning. Validation falls back to Strategy A when Strategy C does not improve performance.

Two additional datasets are used to examine the feasibility of applying TDE to new buildings and related cooling load forecasting tasks.

## Main results

Across the 240 combinations, TDE reduced CVRMSE by an average of **10.16%** compared with the traditional LSTM, and **79.58%** of the combinations improved.

- With 1 to 7 days of target training data, the mean CVRMSE improvement was **4.18%**, and 69.17% of the combinations improved.
- With 10 to 28 days of target training data, the mean improvement increased to **16.13%**, and 90.00% of the combinations improved.
- Residual trajectory generation made the largest contribution among the tested components. It increased the mean CVRMSE improvement from 9.07% to 10.16% and the percentage of improved combinations from 61.67% to 79.58% compared with independent-window generation.
- The improvements remained consistent across different weather station sites. Results from the additional datasets further support application to new buildings and related forecasting tasks.

These findings show that TDE can improve cooling load forecasting from limited local measurements without relying on source-building data.

## Data

The main experiment uses office-building chilled-water meter data, metadata, and weather records from the **Building Data Genome Project 2 (BDG2)**:

- Dataset: <https://www.kaggle.com/datasets/claytonmiller/buildingdatagenomeproject2>
- Reference: Miller, C. et al. *The Building Data Genome Project 2, energy meter data from the ASHRAE Great Energy Predictor III competition*. Scientific Data 7, 368 (2020). <https://doi.org/10.1038/s41597-020-00712-x>

The exploratory external cases use:

- **LBNL Building 59:** <https://bbd.labworks.org/ds/bbd/lbnlbldg59>
- **TUM-EMT Open Energy Data Collection:** <https://collab.dvb.bayern/spaces/TUMenmantech/pages/557810667/TUM-EMT+Open+Energy+Data+Collection>

Raw datasets are not redistributed in this repository. Users must download them from the original providers and follow the corresponding data licenses and terms of use. Processing scripts and dataset instructions will be included in the code release.

## Expected repository structure

```text
target-domain-enhancement/
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── .gitignore
├── configs/
│   ├── main_experiment.yaml
│   ├── ablation.yaml
│   └── external_cases.yaml
├── data/
│   ├── README.md
│   ├── raw/
│   ├── external/
│   ├── interim/
│   └── processed/
├── src/
│   ├── preprocessing/
│   ├── features/
│   ├── generation/
│   ├── screening/
│   ├── ssl/
│   ├── forecasting/
│   └── evaluation/
├── scripts/
│   ├── prepare_data.py
│   ├── run_main_experiment.py
│   ├── run_ablations.py
│   ├── run_external_cases.py
│   └── generate_figures.py
├── results/
│   ├── README.md
│   └── summary/
└── tests/
```

The final directory names and commands may be adjusted during code organization, but the release will preserve the complete workflow used in the manuscript.

## Technical requirements

- Python 3.9.7
- NumPy 2.0.2
- pandas 2.2.3
- Matplotlib 3.9.4
- scikit-learn 1.6.0
- PyTorch 2.5.1
- CUDA 11.8

## Reproduction

After the code release, the intended workflow will be:

```bash
# Install dependencies
pip install -r requirements.txt

# Prepare the downloaded datasets
python scripts/prepare_data.py

# Run the 30-building experiment
python scripts/run_main_experiment.py

# Run module-level ablations
python scripts/run_ablations.py

# Run the external cases
python scripts/run_external_cases.py

# Reproduce manuscript figures and summary tables
python scripts/generate_figures.py
```

Detailed configuration files, expected inputs, random seeds, output paths, and figure-generation instructions will be supplied with the organized code release.

## Citation

If you use this repository, please cite the associated manuscript. The final journal citation and DOI will be added after publication.

```bibtex
@article{liu2026tde,
  title   = {Building cooling load forecasting with limited data: A few-shot target domain enhancement (TDE) framework},
  author  = {Liu, Jiakai and Chen, Yongbao and Luo, Jiahang and Chen, Zhe},
  journal = {Manuscript submitted for publication},
  year    = {2026}
}
```

## License

The source code will be released under the MIT License. Dataset copyrights and licenses remain with the original data providers.

## Contact

- **Questions about the paper:** Yongbao Chen, `chenyongbao@usst.edu.cn`
- **Questions about the code:** Jiakai Liu, `1602252955@qq.com`
- University of Shanghai for Science and Technology

Repository updates and release information will be posted after manuscript acceptance.

## Reproducibility commitment

The public release will include:

1. the implementation used for the main experiment and ablation studies;
2. preprocessing and feature-construction scripts;
3. residual generation, candidate screening, SSL pretraining, and fine-tuning code;
4. experiment configurations and fixed random seeds;
5. compact result summaries and scripts for reproducing the manuscript figures;
6. instructions for preparing the external datasets.
