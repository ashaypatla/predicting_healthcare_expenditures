# Data

The dataset used in this project is **not included** in this repository due to file size. Follow the steps below to download it and set it up locally.

---

## Dataset

**Medical Expenditure Panel Survey (MEPS) 2022 — Full Year Consolidated File (HC-243)**

The MEPS Full-Year Consolidated file contains data on healthcare utilization, expenditures, insurance coverage, and demographic characteristics for the U.S. civilian non-institutionalized population.

---

## Download Instructions

1. Go to the MEPS data download page:  
   https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-243

2. Download the **SAS Transport File (.ssp)** or **CSV** format depending on your preference.

3. Place the downloaded file in this `/data` directory.

4. Rename the file to:
   ```
   HC-243.csv
   ```
   (or update the file path in the notebook to match your filename)

---

## Variables Used

| Variable | Name | Type | Description |
|---|---|---|---|
| `TOTEXP22` | Total Annual Healthcare Expenditures | Numeric | Total medical spending across all services — target variable. Log-transformed for modeling. |
| `AGE22X` | Age | Numeric | Age of respondent as of end of survey year |
| `EDUCYR` | Years of Education | Numeric | Total years of completed education |
| `SEX` | Sex | Categorical | Binary indicator of respondent's sex |
| `RACEV2X` | Race / Ethnicity | Categorical | Self-reported race/ethnicity category |
| `REGION22` | Census Region | Categorical | Geographic region of residence within the U.S. |
| `POVCAT22` | Poverty Status Category | Categorical | Household income relative to federal poverty thresholds |
| `MARRY22X` | Marital Status | Categorical | Respondent's marital status as of survey year |
| `INSURC22` | Insurance Coverage | Categorical | Primary health insurance coverage type (private, public-only, or uninsured) |

All variable definitions and coding conventions follow the official MEPS HC-243 Full-Year Consolidated file documentation, available at the link above.

---

## Notes

- Negative values in MEPS data represent non-response or inapplicable codes and are treated as missing (`NaN`) during preprocessing.
- The target variable `TOTEXP22` is highly right-skewed. A `log1p` transformation is applied before modeling.
- Chronic condition indicator columns (variables ending in `DX`) are used for feature engineering and are included in the full dataset download.
