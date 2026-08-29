# DM2 — Wearable & Tabular Data Mining

Data Mining 2 project developed at the **University of Pisa** (Academic Year 2025–2026).

This repository presents an end-to-end analysis of the **Child Mind Institute (CMI)** dataset, combining participant-level tabular information with wearable sensor time series to study problematic internet use and related physical/behavioral outcomes.

## Project at a Glance

| Area | Methods |
|---|---|
| Data preparation | cleaning, missing-value analysis, KNN/median imputation, scaling, feature engineering |
| Outlier detection | HBOS, LOF, KNN |
| Imbalanced learning | class-imbalance strategies for SII prediction |
| Tabular classification | Logistic Regression, SVM, Neural Network, Random Forest, boosting |
| Regression | Random Forest and XGBoost regression, including BMI analysis |
| Explainability | SHAP, LIME |
| Time-series discovery | Matrix Profile, motifs, discords |
| Time-series clustering | PAA, statistical features, K-Means, hierarchical clustering, DTW |
| Time-series classification | KNN, DTW, Shapelets, MiniROCKET |

The principal classification target is the **Severity Impairment Index (`sii`)**, an ordinal variable:

- `0` — no impairment
- `1` — mild impairment
- `2` — moderate impairment
- `3` — severe impairment

## Dataset

### Tabular component

The project works with **8,460 participant observations** and a broad set of physical, behavioral, fitness, sleep, body-composition and internet-use attributes.

The preparation pipeline covers biologically implausible values, missingness, KNN/median imputation, missingness indicators, duplicate analysis, feature engineering and model-ready transformations.

### Wearable time-series component

The wearable analysis uses multivariate activity/sensor sequences. The processing workflow includes non-wear filtering, missing-value handling, gap-limited interpolation, correlation analysis, subject-level splitting, Piecewise Aggregate Approximation (PAA), and statistical feature extraction.

For the fixed-length representation used in the project, sequences contain **200 time steps and 7 channels**; PAA is also used to obtain a compact 20-segment representation for selected analyses.

> The processed wearable dataset is not redistributed in this repository because of its size. The notebooks document the preprocessing and analysis workflow.

## Analysis Workflow

### 1. Tabular preparation and anomaly analysis

The raw participant data is cleaned and transformed before modelling. HBOS, Local Outlier Factor and KNN-based anomaly detection are then compared to examine different definitions of unusual observations.

### 2. Imbalanced classification

Because `sii` is strongly imbalanced, the project evaluates imbalance-aware learning before comparing supervised classifiers. Both the original four-class target and a grouped three-class formulation are investigated.

Models explored include Logistic Regression, SVM, Neural Networks, Random Forest and boosting approaches.

### 3. Regression and explainability

Random Forest and XGBoost regressors are used for continuous-outcome modelling, including a dedicated BMI analysis. SHAP and LIME are used to interpret model behaviour at global and local levels.

### 4. Motifs and discords

Matrix Profile analysis identifies recurring **motifs** and unusual **discords** in wearable signals, providing a subsequence-level view of repeated and anomalous temporal behaviour.

### 5. Time-series clustering

Alternative representations and distance functions are compared through:

- PAA + K-Means
- statistical-feature K-Means
- DTW hierarchical clustering
- statistical-feature hierarchical clustering

### 6. Time-series classification

Classification experiments include Euclidean and DTW KNN, Shapelet-based models and MiniROCKET. Shapelets are also considered alongside motifs and discords to contrast **discriminative**, **recurring**, and **anomalous** subsequences.

## Repository Structure

```text
DM2-Wearable-Data-Analysis/
├── data/
│   ├── cmi_internet.csv
│   └── data_dictionary.csv
├── notebooks/
│   ├── 01_tabular_data_preprocessing.ipynb
│   ├── 02_tabular_outlier_detection.ipynb
│   ├── 03_tabular_imbalance_learning.ipynb
│   ├── 04_tabular_logistic_regression.ipynb
│   ├── 05_tabular_svm.ipynb
│   ├── 06_tabular_svm_3class.ipynb
│   ├── 07_tabular_neural_network.ipynb
│   ├── 08_tabular_random_forest_shap.ipynb
│   ├── 09_tabular_bmi_regression.ipynb
│   ├── 10_tabular_xgboost_lime.ipynb
│   ├── 11_time_series_preprocessing.ipynb
│   ├── 12_time_series_motifs_discords.ipynb
│   ├── 13_time_series_paa_dtw_clustering.ipynb
│   ├── 14_time_series_feature_clustering.ipynb
│   ├── 15_time_series_knn_shapelets.ipynb
│   └── 16_time_series_minirocket.ipynb
├── report/
│   └── DM2_Wearable_Data_Analysis_Report.pdf
├── .gitignore
└── README.md
```

## Notebook Guide

| # | Notebook | Focus |
|---:|---|---|
| 01 | `01_tabular_data_preprocessing.ipynb` | Cleaning, missingness and preprocessing |
| 02 | `02_tabular_outlier_detection.ipynb` | HBOS, LOF and KNN outliers |
| 03 | `03_tabular_imbalance_learning.ipynb` | Imbalanced learning |
| 04 | `04_tabular_logistic_regression.ipynb` | Logistic Regression |
| 05 | `05_tabular_svm.ipynb` | SVM classification |
| 06 | `06_tabular_svm_3class.ipynb` | Three-class SVM |
| 07 | `07_tabular_neural_network.ipynb` | Neural Network |
| 08 | `08_tabular_random_forest_shap.ipynb` | Random Forest + SHAP |
| 09 | `09_tabular_bmi_regression.ipynb` | BMI regression |
| 10 | `10_tabular_xgboost_lime.ipynb` | XGBoost + LIME |
| 11 | `11_time_series_preprocessing.ipynb` | Wearable preprocessing and EDA |
| 12 | `12_time_series_motifs_discords.ipynb` | Matrix Profile, motifs and discords |
| 13 | `13_time_series_paa_dtw_clustering.ipynb` | PAA and DTW clustering |
| 14 | `14_time_series_feature_clustering.ipynb` | Feature-based clustering |
| 15 | `15_time_series_knn_shapelets.ipynb` | KNN, DTW and Shapelets |
| 16 | `16_time_series_minirocket.ipynb` | MiniROCKET classification |

## Reproducibility

The notebooks are ordered according to the project workflow. Some later time-series notebooks depend on processed wearable arrays produced during preprocessing and therefore require access to the original wearable data.

To reproduce an analysis, open the relevant notebook in Jupyter/Colab and install the packages imported by that notebook. Local environments, credentials, notebook checkpoints and secret files are excluded through `.gitignore`.

## Data Availability

`data/cmi_internet.csv` and `data/data_dictionary.csv` are included for the tabular analysis. The larger processed wearable arrays are intentionally not committed.

Users of the repository should follow the original dataset's terms and usage requirements when obtaining or redistributing source data.

## Full Project Report

The complete methodology, experiments, figures, results and discussion are available in:

**[DM2 Wearable Data Analysis Report](report/DM2_Wearable_Data_Analysis_Report.pdf)**

## Authors

- **Fiza Naeem**
- **Lorena Sorce**
- **Nague Ivane Maeva**

**University of Pisa — Data Mining 2 — Academic Year 2025–2026**
