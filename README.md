# XAI Diabetes Classification Project

## Project overview

The aim of this project is to build and evaluate machine learning models for binary classification of diabetes risk and to interpret model predictions using XAI methods.

The project uses the **Pima Indians Diabetes Dataset**. The target variable is `Outcome`:

- `0` — no diabetes,
- `1` — diabetes.

## Dataset

The dataset contains diagnostic information about patients, including:

- `Pregnancies`,
- `Glucose`,
- `BloodPressure`,
- `SkinThickness`,
- `Insulin`,
- `BMI`,
- `DiabetesPedigreeFunction`,
- `Age`,
- `Outcome`.

## Data preprocessing

During data exploration, values equal to `0` were found in several medical columns:

- `Glucose`,
- `BloodPressure`,
- `SkinThickness`,
- `Insulin`,
- `BMI`.

Since zero values in these columns are difficult to interpret medically and may indicate missing or incorrect measurements, observations containing such values were removed.

After preprocessing, the dataset size was reduced from **768** to **392** observations. This is an important limitation of the project, but it allowed the models to be trained on a cleaner dataset.

The data was split into training and test sets using an 80/20 split with stratification.

## Models

Three classification models were trained and evaluated:

1. **Logistic Regression**
2. **Random Forest**
3. **SVC**

Logistic Regression was used as a naturally interpretable model. Random Forest and SVC were used as more complex models for comparison.

## Model evaluation

The models were evaluated using the following metrics:

- Accuracy,
- Balanced accuracy,
- Precision,
- Recall,
- F1-score,
- ROC AUC.

Additionally, **Stratified K-Fold cross-validation** was used to check the stability of model performance.

On a single train/test split, SVC achieved the highest accuracy, while Random Forest achieved the highest recall for class `1`. In cross-validation, Random Forest achieved the highest mean ROC AUC.

## XAI methods

The following explainability methods were used:

### Logistic Regression

- model coefficients,
- Permutation Importance.

### Random Forest

- Permutation Importance,
- SHAP summary plot,
- SHAP bar plot,
- SHAP waterfall plot,
- LIME,
- PDP / ICE.

### SVC

- model coefficients,
- Permutation Importance.

## Main XAI findings

The most important feature across most methods was **Glucose**. Higher glucose values generally increased the predicted probability of diabetes.

Other relevant features included:

- `BMI`,
- `Age`,
- `DiabetesPedigreeFunction`,
- `Insulin`.

The XAI analysis showed that the models relied on medically meaningful variables, especially glucose level, when predicting diabetes risk.

## Project structure

```text
.
├── data/
│   └── diabetes.csv
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_models_evaluation.ipynb
│   └── 03_xai_interpretation.ipynb
├── outputs/
│   └── figures/
│       ├── logistic_coefficients.png
│       ├── permutation_importance_logistic.png
│       ├── permutation_importance_random_forest.png
│       ├── permutation_importance_svc.png
│       ├── shap_summary_random_forest.png
│       ├── shap_bar_random_forest.png
│       ├── shap_waterfall_random_forest.png
│       ├── lime_random_forest.png
│       ├── pdp_ice_all_features_random_forest.png
│       ├── pdp_ice_glucose_random_forest.png
│       └── svc_coefficients.png
├── README.md
└── REPORT.md
