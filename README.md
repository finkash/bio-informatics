# Leveraging Multiple Health Data Sources for Prediction of Hypertension and Heart Disease using Machine Learning Models

## Overview

This project applies machine learning techniques to predict four major cardiovascular and metabolic conditions — **Hypertension**, **Heart Disease**, **Stroke**, and **Diabetes** — by integrating multiple health datasets into a unified dataset. The study evaluates four classifiers (Logistic Regression, Random Forest, SVC, and Neural Network/MLP) and performs feature importance analysis using mutual information.

---

## Repository Structure

```
bio-informatics/
│
├── Preprocessing.ipynb         # Data cleaning, standardization, and dataset merging
├── Visualization.ipynb         # Histograms, correlation matrix, and pair plots
├── Analysis.ipynb              # Mutual information computation and feature filtering
├── Models.ipynb                # Training and evaluation of ML classifiers
├── Results.ipynb               # Summary of results and comparisons
│
├── combined_dataset.csv        # Merged dataset from all 5 source datasets
├── DatasetsMetadata.csv        # Metadata for individual source datasets
├── DatasetsMetadata.xlsx       # Metadata (Excel format)
│
├── Diabetes_filtered.csv       # Feature-filtered dataset for Diabetes prediction
├── Heart_Disease_filtered.csv  # Feature-filtered dataset for Heart Disease prediction
├── Hypertension_filtered.csv   # Feature-filtered dataset for Hypertension prediction
├── Stroke_filtered.csv         # Feature-filtered dataset for Stroke prediction
│
├── all_features_results.txt    # Accuracy results for all conditions (all features)
│
└── Paper_-_216150.pdf          # Full research paper
```

---

## Datasets

Five publicly available datasets were combined into a single unified dataset:

| Dataset | Source | Samples |
|---|---|---|
| Heart Failure Prediction | Kaggle (Chicco & Jurman) | 298 |
| Diabetes Health Indicators | BRFSS 2015 / Kaggle | 253,679 |
| Heart Stroke Dataset | Kaggle (Lirilkumar Amal) | 43,399 |
| Identification of Risk Factors for Heart Disease | Swiss Heart Disease Study | 916 |
| Hypertension Incidence Dataset | Kaggle (Kholmirzaev) | 21,612 |

---

## Features

The combined dataset contains the following 12 standardized features:

| Feature | Type | Description |
|---|---|---|
| Age | Integer | Patient age at time of visit |
| Sex | Boolean | 0 = Female, 1 = Male |
| Hypertension | Boolean | Blood pressure ≥ 130/80 mmHg |
| Diabetes | Boolean | Chronic high blood sugar condition |
| Smoking | Boolean | Current or past smoker |
| High Cholesterol | Boolean | Elevated cholesterol levels |
| Heart Disease | Boolean | Presence of heart disease |
| BMI | Float | Weight (kg) / Height² (m²) |
| Stroke | Boolean | History of stroke |
| Physical Activity | Boolean | Active 2+ times/week |
| Fasting Blood Sugar | Boolean | ≥ 126 mg/dL indicates diabetes |
| Chest Pain Type | Integer | 1 = typical angina, 2 = atypical, 3 = non-anginal, 4 = asymptomatic |

Missing values are encoded as `-1`. Rows where the target variable is `-1` and columns where all values are `-1` are removed before training.

---

## Methodology

### Preprocessing (`Preprocessing.ipynb`)
- Filtered relevant features from each source dataset
- Standardized differing value formats (boolean/integer) using medical guidelines
- Merged all datasets into `combined_dataset.csv`
- Encoded missing values as `-1`

### Visualization (`Visualization.ipynb`)
- Feature distribution histograms
- Correlation matrix heatmap
- Pair plots for relationship analysis

### Feature Selection (`Analysis.ipynb`)
- Computed **mutual information** between each feature and each target variable
- Generated per-condition filtered CSVs for downstream modeling

### Classification (`Models.ipynb`)
Four classifiers were trained and evaluated on each condition:
- **Logistic Regression (LR)**
- **Random Forest (RF)**
- **Support Vector Classifier (SVC)**
- **Neural Network / MLP** — two hidden layers, 400 neurons each

---

## Results

### Model Accuracy (All Features)

| Condition | LR | RF | SVC | MLP |
|---|---|---|---|---|
| Hypertension | 74.01% | 71.90% | 74.20% | **74.40%** |
| Heart Disease | 91.71% | 90.47% | 91.83% | **91.88%** |
| Stroke | 96.48% | 95.75% | 96.48% | **96.48%** |
| Diabetes | 87.06% | 85.53% | 87.03% | **87.35%** |

The Neural Network (MLP) consistently achieved the highest or tied-highest accuracy across all four conditions.

### Top Features by Mutual Information

| Condition | Top Features |
|---|---|
| Hypertension | Age (0.076), High Cholesterol (0.074), Fasting Blood Sugar (0.071) |
| Heart Disease | Chest Pain Type (0.083), Fasting Blood Sugar (0.072), Hypertension (0.042) |
| Stroke | Fasting Blood Sugar (0.075), Smoking (0.041), Physical Activity (0.040) |
| Diabetes | Smoking (0.056), Hypertension (0.055), Physical Activity (0.049) |

---

## Key Findings

- **Neural Networks** slightly outperform other classifiers across all conditions.
- **Fasting blood sugar** is the most consistently predictive feature across all four diseases.
- **Chest pain type** is the strongest predictor for heart disease.
- **Smoking** and **hypertension** are the leading risk factors for diabetes prediction.
---

## Future Work

- Incorporate additional and more diverse health datasets
- Explore deep learning architectures for improved accuracy
- Extend predictions to additional health conditions
- Investigate longitudinal data to model disease progression over time

---

## Reference

Zorica Nikov. *Leveraging Multiple Health Data Sources for Prediction of Hypertension and Heart Disease using Machine Learning Models.* Faculty of Computer Science and Engineering, Ss. Cyril and Methodius University of Skopje, 2024.
