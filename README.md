# Ames Housing Data Preprocessing Project

## 📌 Overview
This project preprocesses the **Ames Housing dataset**, a popular dataset for regression tasks in real estate price prediction.  
The preprocessing steps follow best practices to ensure **data quality, consistency, and modeling readiness**.

---

## 📂 Dataset
- **Source:** [Ames Housing Dataset (Kaggle)](https://www.kaggle.com/datasets/shashanknecrothapa/ames-housing-dataset)
- **Observations:** 2930  
- **Variables:** 82 (numeric & categorical)  
- **Target:** `SalePrice` (continuous variable)

A **data dictionary** is provided in the original dataset documentation.

---

## 🛠 Tools & Libraries
- **Python 3.9+**
- **pandas** – data manipulation  
- **numpy** – numerical operations  
- **scikit-learn** – preprocessing, feature selection, scaling  
- **matplotlib / seaborn** – visualization  
- **category_encoders** – advanced categorical encoding  
- **jupyter notebook** – interactive development  

Install them via:
```bash
pip install -r requirements.txt
```

⚙️ Preprocessing Workflow
1. Data Exploration & Cleaning
Converted inconsistent data types to proper formats.

Detected and removed duplicate rows.

Managed missing values:

Dropped columns with >50% missingness (Pool QC, Misc Feature, etc.).

Imputed numeric columns using median or regression imputation.

Imputed categorical columns with mode or most frequent category.
Reference: Preprocessing Techniques

2. Outlier Detection & Treatment
Detection Methods:

Z-score (|Z| > 3)

IQR rule ([Q1 - 1.5×IQR, Q3 + 1.5×IQR])

Treatment:

Winsorization for extreme numeric outliers.

Log transformation for skewed variables (SalePrice, LotFrontage).
Reference: Outlier Detection Notes

3. Categorical Encoding
Nominal variables (unordered): One-Hot Encoding & Frequency Encoding.

Ordinal variables (ordered): Ordinal Encoding based on natural rank.

High cardinality features: Target Encoding with out-of-fold strategy to prevent leakage.
Reference: Categorical Encoding

4. Feature Engineering
Created additional features:

HouseAge = YrSold - YearBuilt

RemodAge = YrSold - YearRemodAdd

TotalSF = 1stFlrSF + 2ndFlrSF + TotalBsmtSF

QualityRatio = OverallQual / OverallCond

Dropped redundant variables used in derived features.

5. Scaling & Standardization
Applied StandardScaler for normally distributed numeric variables.

Applied MinMaxScaler for bounded-range features.

Verified distribution shifts using histograms.

6. Feature Selection
Filter methods: Variance threshold, Pearson correlation (|r| > 0.8).

Wrapper methods: Recursive Feature Elimination (RFE).

Embedded methods: Lasso (L1 regularization), Random Forest importance scores.
Reference: Feature Selection

🔄 Pipeline Summary
mermaid
Copier
Modifier
graph TD
    A[Raw Dataset] --> B[Data Cleaning]
    B --> C[Missing Value Imputation]
    C --> D[Outlier Detection & Treatment]
    D --> E[Categorical Encoding]
    E --> F[Feature Engineering]
    F --> G[Scaling & Standardization]
    G --> H[Feature Selection]
    H --> I[Model-Ready Dataset]


