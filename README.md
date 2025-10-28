# 📊  Finance: Credit Risk Model

### End-to-End Credit Risk Modelling System  
An end-to-end Credit Risk Modelling solution built for **Finance Companies** to predict **loan default probability**, generate **credit scores (300–900)**, and assign **risk ratings**.  
The project covers data preprocessing, feature engineering, model optimization, evaluation, and deployment via **Streamlit**.

---

## 🧭 Project Overview

**Purpose:**  
To assess loan default risk and simulate a real-world credit scoring system.  
The model predicts default probability and converts it into a **credit score and rating** for easy interpretation.

**Domain:** Finance / Machine Learning / Risk Analytics  
**Deployment:** Streamlit Web Application  
**Model Type:** Classification (Binary — Default vs Non-default)

---

## ⚙️ Workflow

### 1️⃣ Data Preparation
- Merged `customers.csv`, `loans.csv`, and `bureau_data.csv` (~50k records each).  
- Cleaned missing and inconsistent data.  
- Removed outliers (processing fee > 3% of loan amount).  
- Standardized categorical entries.

### 2️⃣ Feature Engineering
Key features created:
- Loan-to-Income Ratio  
- Delinquency Ratio  
- Average DPD per Delinquency  
- One-hot encoded features for Residence Type, Loan Purpose, and Loan Type

### 3️⃣ Feature Selection
- **VIF** for multicollinearity reduction  
- **Information Value (IV)** for variable importance (IV > 0.02)

### 4️⃣ Handling Class Imbalance
- Used **SMOTETomek** resampling for balanced training data.

### 5️⃣ Model Development
Algorithms used:
- Logistic Regression  
- Random Forest  
- XGBoost (tuned with **Optuna**)

### 6️⃣ Model Evaluation
Metrics evaluated:
- Accuracy  
- F1-score  
- Precision  
- Recall  
- AUC-ROC  
- Gini  
- KS Statistic  

---

## 🧠 Model Details

### 🟢 XGBoost (Best Performing Model)
**Description:** Optuna-tuned XGBoost model with highest accuracy and balanced performance.

**Best Trial:**
- **F1-score:** 0.9771  
- **Parameters:**
  - λ: 3.956  
  - α: 0.113  
  - Subsample: 0.931  
  - Colsample_bytree: 0.903  
  - Max Depth: 10  
  - Eta: 0.273  
  - Gamma: 0.486  
  - Scale_pos_weight: 2.47  
  - Min_child_weight: 3  
  - Max_delta_step: 2  

**Classification Report:**
| Metric | Class 0 | Class 1 |
|--------|----------|----------|
| Precision | 0.99 | 0.71 |
| Recall | 0.97 | 0.85 |
| F1-score | 0.98 | 0.78 |

**Performance:**
- Accuracy: 0.96  
- AUC: 0.9837  
- Gini: 0.9674  
- KS Statistic: 85.89  

---

### 🔵 Logistic Regression (Deployed Model)
**Description:** Interpretable model chosen for deployment due to high explainability.  

**Classification Report:**
| Metric | Class 0 | Class 1 |
|--------|----------|----------|
| Precision | 0.99 | 0.55 |
| Recall | 0.93 | 0.94 |
| F1-score | 0.96 | 0.69 |

**Performance:**
- Accuracy: 0.93  
- AUC: 0.9837  
- Gini: 0.967  
- KS Statistic: 85.9  

**Explainability:** High (white-box model with interpretable coefficients)  
**Deployment Status:** ✅ Deployed via Streamlit  

---

## 📈 Evaluation Insights

### 🧮 Decile Analysis Summary
| Decile | Probability Range | Event Rate (%) | KS Value |
|:------:|:----------------:|:--------------:|:--------:|
| 9 | 0.812 – 1.000 | 71.84 | 80.53 |
| 8 | 0.240 – 0.811 | 12.80 | 85.89 |
| 7 | 0.040 – 0.240 | 0.88 | 76.07 |
| 6 | 0.007 – 0.040 | 0.40 | 65.64 |

### 💳 Credit Score Conversion
| Credit Score Range | Rating | Interpretation |
|:-------------------:|:-------:|:---------------|
| 300–499 | Poor | High default risk |
| 500–649 | Average | Medium risk |
| 650–749 | Good | Low risk |
| 750–900 | Excellent | Very low risk |

---

## 🌐 Streamlit Web App

**Description:**  
Interactive web app where users input parameters (age, income, loan amount, tenure, DPD, loan type) to get:
- Default Probability  
- Credit Score (300–900)  
- Risk Rating (Poor / Average / Good / Excellent)

**Key Files:**
- `main.py`  
- `prediction_helper.py`

**Deployment Model:** Logistic Regression  
**Libraries Used:** `streamlit`, `joblib`, `pandas`, `numpy`, `scikit-learn`

---


