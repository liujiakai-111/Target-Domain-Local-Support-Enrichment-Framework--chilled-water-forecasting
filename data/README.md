# Data preparation

The raw datasets used in this study are not redistributed in this repository.

## Main dataset

The main experiment uses office-building chilled-water meter data, metadata, and weather records from the Building Data Genome Project 2:

- Dataset: https://www.kaggle.com/datasets/claytonmiller/buildingdatagenomeproject2
- Reference: https://doi.org/10.1038/s41597-020-00712-x

## External datasets

The exploratory cases use:

- LBNL Building 59: https://bbd.labworks.org/ds/bbd/lbnlbldg59
- ORNL Flexible Research Platform data, accessed through the TUM-EMT Open Energy Data Collection: https://collab.dvb.bayern/spaces/TUMenmantech/pages/557810667/TUM-EMT+Open+Energy+Data+Collection

## Local directory structure

After downloading the datasets, place them under:

```text
data/
├── raw/
│   └── bdg2/
├── external/
│   ├── lbnl_building59/
│   └── ornl_frp/
├── interim/
├── processed/
└── README.md
```

The exact required filenames and preprocessing commands will be documented with the public code release.

Raw and processed datasets are excluded from Git tracking. Users must comply with the licenses and terms specified by the original data providers.
