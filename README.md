# DM2 – Wearable Data Analysis

Data Mining 2 project developed at the University of Pisa, Academic Year 2025–2026.

## Project Overview

This project analyzes the Child Mind Institute (CMI) dataset to investigate problematic internet use in children and adolescents.

The main target is the Severity Impairment Index (`sii`), an ordinal variable ranging from:

- 0 – No impairment
- 1 – Mild impairment
- 2 – Moderate impairment
- 3 – Severe impairment

The project combines tabular and wearable time-series data and applies data preprocessing, outlier detection, imbalanced learning, classification, regression, explainability, clustering, motif/discord discovery, and time-series classification.

## Dataset

### Tabular Data

The tabular dataset contains 8,460 participants aged 5–22 and includes physical, behavioral, fitness, sleep, body-composition, and internet-use related attributes.

The preprocessing pipeline includes:

- Detection of biologically impossible values
- Missing-value handling
- KNN and median imputation
- Missingness indicators
- Feature engineering
- Duplicate analysis
- Data scaling and preparation

### Time-Series Data

The wearable component contains multivariate time series representing physical activity and sensor measurements.

The time-series preprocessing includes:

- Non-wear detection and filtering
- Missing-value handling
- Gap-limited interpolation
- Signal correlation analysis
- Subject-level train/test splitting
- Piecewise Aggregate Approximation (PAA)
- Statistical feature extraction

PAA reduces the original 200-step sequences to 20 segments while preserving their overall temporal structure.

## Analysis Pipeline

### 1. Tabular Data Preparation

The raw tabular data is cleaned and transformed before modelling. Invalid physiological measurements are replaced with missing values, missing data is imputed, and additional features are engineered.

### 2. Outlier Detection

Three outlier-detection approaches are investigated:

- HBOS
- Local Outlier Factor (LOF)
- K-Nearest Neighbors (KNN)

Their detections are compared to identify structurally unusual observations and evaluate agreement between different definitions of anomalous behavior.

### 3. Imbalanced Learning

Because the SII target is strongly imbalanced, several strategies are evaluated to improve minority-class prediction.

### 4. Tabular Classification

Several supervised-learning models are investigated:

- Logistic Regression
- Support Vector Machine (SVM)
- Neural Network
- Random Forest
- XGBoost
- AdaBoost

Both the original four-class SII formulation and a grouped three-class formulation are investigated.

### 5. Regression

Regression models are used to study continuous physical outcomes and their relationship with problematic internet use.

Models include:

- Random Forest Regressor
- XGBoost Regressor

A dedicated analysis investigates prediction of physical BMI and its relationship with SII.

### 6. Explainable AI

Model behavior is interpreted using:

- SHAP
- LIME

These methods are used to investigate feature importance and individual feature contributions.

### 7. Time-Series Motifs and Discords

Matrix Profile-based analysis is used to identify:

- Motifs – recurring temporal patterns
- Discords – unusual or anomalous subsequences

### 8. Time-Series Clustering

Multiple representations and clustering strategies are compared:

- PAA + K-Means
- Statistical Feature K-Means
- DTW Hierarchical Clustering
- Statistical Feature Hierarchical Clustering

### 9. Time-Series Classification

Time-series classification is investigated using:

- KNN with Euclidean distance
- KNN with DTW distance
- Shapelet-based classification
- MiniROCKET

Shapelets are also compared with motifs and discords to investigate whether discriminative subsequences correspond to recurring or anomalous temporal behavior.

## Repository Structure

DM2-Wearable-Data-Analysis/

- `data/`
  - `cmi_internet.csv`
  - `data_dictionary.csv`

- `notebooks/`
  - `01_tabular_data_preprocessing.ipynb`
  - `02_tabular_outlier_detection.ipynb`
  - `03_tabular_imbalance_learning.ipynb`
  - `04_tabular_logistic_regression.ipynb`
  - `05_tabular_svm.ipynb`
  - `06_tabular_svm_3class.ipynb`
  - `07_tabular_neural_network.ipynb`
  - `08_tabular_random_forest_shap.ipynb`
  - `09_tabular_bmi_regression.ipynb`
  - `10_tabular_xgboost_lime.ipynb`
  - `11_time_series_preprocessing.ipynb`
  - `12_time_series_motifs_discords.ipynb`
  - `13_time_series_paa_dtw_clustering.ipynb`
  - `14_time_series_feature_clustering.ipynb`
  - `15_time_series_knn_shapelets.ipynb`
  - `16_time_series_minirocket.ipynb`

- `report/`
  - `DM2_Wearable_Data_Analysis_Report.pdf`

- `README.md`

## Notebook Guide

| Notebook | Analysis |
|---|---|
| 01 | Tabular data cleaning and preprocessing |
| 02 | HBOS, LOF and KNN outlier detection |
| 03 | Imbalanced-learning analysis |
| 04 | Logistic Regression classification |
| 05 | SVM classification |
| 06 | Three-class SVM classification |
| 07 | Neural Network classification |
| 08 | Random Forest and SHAP explainability |
| 09 | BMI regression analysis |
| 10 | XGBoost regression and LIME explainability |
| 11 | Time-series preprocessing and exploratory analysis |
| 12 | Matrix Profile, motifs and discords |
| 13 | PAA and DTW-based clustering |
| 14 | Statistical feature-based clustering |
| 15 | KNN and Shapelet time-series classification |
| 16 | MiniROCKET time-series classification |

## Data Availability

The tabular dataset and data dictionary are included in the `data/` directory.

The processed wearable time-series dataset is not stored directly in the repository because of its larger file size. The time-series notebooks document the processing and analysis performed on this data.

## Project Report

The complete methodology, experiments, results, figures, and discussion are available in:

`report/DM2_Wearable_Data_Analysis_Report.pdf`

## Authors

- Fiza Naeem
- Lorena Sorce
- Nague Ivane Maeva

**University of Pisa**  
**Data Mining 2**  
**Academic Year 2025–2026**
