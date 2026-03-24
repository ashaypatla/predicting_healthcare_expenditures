# Predicting Healthcare Expenditures

A machine learning project that predicts annual healthcare expenditures using the 2022 Medical Expenditure Panel Survey (MEPS), with a focus on risk stratification and identifying key demographic and health drivers of spending.

---

## Overview

Healthcare costs are highly skewed — a small proportion of individuals account for a disproportionately large share of total spending. This project trains and compares multiple regression models to predict individual annual expenditures, using demographic, insurance, socioeconomic, and chronic condition features from MEPS survey data.

---

## Dataset

**Medical Expenditure Panel Survey (MEPS) 2022 — Full Year Consolidated File (HC-243)**  
Source: https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-243

| Variable | Description |
|---|---|
| `TOTEXP22` | Total annual healthcare expenditures (target variable) |
| `AGE22X` | Age of respondent |
| `EDUCYR` | Years of completed education |
| `SEX` | Sex (categorical) |
| `RACEV2X` | Race / ethnicity (categorical) |
| `REGION22` | Census region (categorical) |
| `POVCAT22` | Poverty status category |
| `MARRY22X` | Marital status |
| `INSURC22` | Insurance coverage type |

Variable definitions follow official MEPS Full-Year Consolidated file documentation.

---

## Preprocessing

- Replaced MEPS-specific negative values (non-response codes) with `NaN` and dropped rows with missing predictors
- Applied `log1p` transformation to the target variable to reduce right skew
- One-hot encoded categorical features (first category dropped to prevent multicollinearity)
- Standardized numeric features to zero mean and unit variance

---

## Feature Engineering

A **chronic condition count** feature was engineered from diagnosis indicator columns (variables ending in `DX`) to capture health status beyond demographics. Conditions selected were chronic, cost-driving, and applicable across all ages. This feature was summed per patient and added as a numeric predictor, with the scaler and train/test splits re-applied afterward.

---

## Models

| Model | Notes |
|---|---|
| Baseline (mean predictor) | Naive benchmark |
| Linear Regression | 26.5% variance explained — demographic features provide signal |
| Ridge Regression | Performed similarly to linear regression; overfitting was not the primary issue |
| Random Forest | Underperformed linear models — feature signal was the limiting factor |
| Gradient Boosting | Best performer — captured weak nonlinear relationships via residual fitting |

---

## Evaluation

Models were evaluated on the log-transformed target variable using the following metrics:

| Metric | Score |
|---|---|
| R² | 0.338 |
| RMSE | 2.620 |
| MAE | 1.955 |

The final model explains ~33.8% of variance in log-transformed healthcare expenditures. Metrics are reported on the log scale given the `log1p` transformation applied to the target variable.

---

## Key Findings

- Demographic and insurance features alone explain ~26.5% of expenditure variance
- Performance limitations stem from feature signal rather than model flexibility
- Gradient Boosting produced the best results, with further gains after adding chronic condition count
- Healthcare spending is driven by nonlinear interactions not fully captured by demographic features alone
- The final Gradient Boosting model with chronic condition count achieved an R² of 0.338,
  up from 0.265 with demographic features alone

---

## How to Run

**1. Install dependencies**
```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

**2. Download the dataset**  
Download `HC-243` from the MEPS website and place it in the project directory.

**3. Run the notebook**  
Open `predicting_healthcare_spending.ipynb` in Jupyter Notebook or VS Code and run all cells.

---

## Tech Stack

- Python, Pandas, NumPy
- Scikit-learn (Linear Regression, Ridge, Random Forest, Gradient Boosting)
- Matplotlib / Seaborn

---

## Author

Ashay Patla
