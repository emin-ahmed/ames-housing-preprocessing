# Ames Housing Data Preprocessing Project

## 📌 Overview
This project focuses on **preprocessing the Ames Housing dataset** to prepare it for machine learning tasks.  
The pipeline covers **all steps**, from initial exploration to final feature selection, ensuring a **clean, robust, and model-ready dataset**.

---

## 📂 Dataset
- **Source:** [Ames Housing Dataset (Kaggle)](https://www.kaggle.com/datasets/shashanknecrothapa/ames-housing-dataset)
- **Observations:** 2930  
- **Variables:** 82 (numeric & categorical)  
- **Target:** `SalePrice` (continuous)

A **data dictionary** is available in the original dataset.

---

## 🛠 Tools & Libraries
- **Python 3.9+**
- **pandas**, **numpy** – Data manipulation & numerical computation  
- **scikit-learn** – Preprocessing, scaling, feature selection  
- **category_encoders** – Advanced categorical encoding  
- **matplotlib**, **seaborn** – Visualization  
- **jupyter notebook** – Interactive analysis  

---

## ⚙️ Preprocessing Pipeline

### 1. Data Exploration & Cleaning
**Objectives:**  
- Understand data structure, detect inconsistencies, and handle missing or duplicate records.

**Steps Implemented:**  
- Converted inconsistent data types (e.g., string to numeric).  
- Removed duplicate rows (if any).  
- Managed missing values:
  - Dropped columns with >50% missing values (`Pool QC`, `Misc Feature`, etc.).
  - Imputed numerical features with median or regression-based imputation.
  - Imputed categorical features with the mode or most frequent category.  

_Reference: [Preprocessing Techniques](pretretementDonnees-pages-2.pdf)_

---

### 2. Outlier Detection & Treatment
**Objectives:**  
- Detect and handle extreme values to prevent model bias.

**Techniques Used:**  
- **Z-score** (|Z| > 3) for symmetric distributions.  
- **IQR rule** (`[Q1 - 1.5×IQR, Q3 + 1.5×IQR]`) for skewed variables.  

**Treatments:**  
- Winsorization for extreme outliers.  
- Log transformations for highly skewed variables like `SalePrice` and `LotFrontage`.  

_Reference: [Outlier Detection](outliers.pdf)_

---

### 3. Categorical Encoding
**Objectives:**  
- Convert categorical variables into numerical formats usable by ML models.

**Encoding Techniques:**  
- **Nominal features**: One-Hot Encoding (low cardinality) or Frequency Encoding (high cardinality).  
- **Ordinal features**: Ordinal Encoding (based on natural ranking).  
- **High cardinality features**: Target Encoding with out-of-fold strategy to avoid leakage.  

_Reference: [Categorical Encoding](Encodage_categoriel_et_text_preprocessing.pdf)_

---

### 4. Feature Engineering
**Objectives:**  
- Create meaningful derived variables and remove redundant ones.

**New Features:**  
- `HouseAge = YrSold - YearBuilt`  
- `RemodAge = YrSold - YearRemodAdd`  
- `TotalSF = 1stFlrSF + 2ndFlrSF + TotalBsmtSF`  
- `QualityRatio = OverallQual / OverallCond`

**Redundant Features Removed:**  
- Dropped original features used to compute new derived variables to reduce multicollinearity.

---

### 5. Scaling & Standardization
**Objectives:**  
- Normalize feature ranges to ensure model stability.

**Scaling Techniques:**  
- `StandardScaler` for normally distributed variables.  
- `MinMaxScaler` for bounded-range variables.  

**Validation:**  
- Compared distributions before and after scaling using histograms.

---

### 6. Feature Selection
**Objectives:**  
- Reduce dimensionality and remove redundant or irrelevant variables.

**Techniques Used:**  
- **Filter methods:** Variance threshold & Pearson correlation (|r| > 0.8).  
- **Wrapper methods:** Recursive Feature Elimination (RFE).  
- **Embedded methods:** Lasso (L1) regularization and Random Forest importance scores.  

_Reference: [Feature Selection](feature_selection.pdf)_

---

## 🔄 Pipeline Summary
```mermaid
graph TD
    A[Raw Dataset] --> B[Data Cleaning & Missing Value Handling]
    B --> C[Outlier Detection & Treatment]
    C --> D[Categorical Encoding]
    D --> E[Feature Engineering]
    E --> F[Scaling & Standardization]
    F --> G[Feature Selection]
    G --> H[Model-Ready Dataset]
