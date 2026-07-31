# Customer Churn Prediction — Telecom Analytics Tool

**3MTT Nigeria | Cohort 3 | Wesonline Mentorship Programme**
**Track:** Advanced Data Analysis & Visualization
**Author:** Okereke Obaji Eze | okereke.obaji@yahoo.com |
**Location:** Lagos, Nigeria

---

## Project Overview

This project builds a machine learning pipeline to predict customer churn for telecom operators. Using the publicly available IBM Telco Customer Churn dataset as a proxy, the project demonstrates how Nigerian telecom operators (MTN, Airtel, Glo, 9mobile) can adopt a data-driven approach to identify at-risk subscribers before they disconnect — enabling targeted, cost-effective retention interventions.

> **Data Provenance Notice:** This model was trained on the publicly available IBM Telco Customer Churn dataset (sourced from Kaggle, 7,043 original rows). This dataset serves as a validated proxy for telecom churn modelling. The pipeline, feature engineering, and model architecture are directly applicable to Nigerian operator data, but the model would require retraining on local subscriber records before live deployment with any Nigerian telecom provider.

---

## Problem Statement

Nigeria's telecom industry serves over 220 million subscribers and contributes approximately 14% to GDP. Annual churn rates of 20–30% are common across the sector. Without affordable predictive tools, operators rely on reactive retention — responding after customers have already left. This wastes budget and accelerates revenue loss in one of Africa's most competitive markets.

---

## Dataset

| Attribute | Detail |
|---|---|
| Source | IBM Telco Customer Churn Dataset (Kaggle) |
| Original Records | 7,043 rows |
| Records After Cleaning | 7,032 rows (11 removed — missing TotalCharges) |
| Features | 21 columns (20 after dropping CustomerID) |
| Target Variable | Churn (Yes → 1, No → 0) |
| Class Distribution | 73.42% No Churn / 26.58% Churn |

**Dataset link:** https://www.kaggle.com/datasets/blastchar/telco-customer-churn

---

## Project Pipeline

```

![Architecture Diagram](architecture_diagram)



Raw CSV Data
    │
    ▼
Data Cleaning
(Convert TotalCharges to numeric, drop 11 nulls,
 encode Churn Yes/No → 1/0, drop CustomerID)
    │
    ▼
Exploratory Data Analysis (EDA)
(Churn by contract type, tenure, monthly charges,
 internet service — using Matplotlib & Seaborn)
    │
    ▼
Feature Engineering
(One-hot encoding of all categorical columns,
 80/20 train-test split, StandardScaler normalisation)
    │
    ▼
Model Training
(Logistic Regression + Random Forest Classifier)
    │
    ▼
Model Evaluation
(Accuracy, Precision, Recall, F1-Score, AUC-ROC,
 Confusion Matrix, ROC Curve)
    │
    ▼
Feature Importance Analysis
(Random Forest feature_importances_)
    │
    ▼
Power BI Dashboard
(8 interactive visuals — churn rate, contract type,
 tenure trend, charge bands, internet service, top drivers)
    │
    ▼
Export Results
(CSV outputs for dashboard integration)
```

---

## Model Performance

### Validation Methodology
The dataset was split into **80% training (5,625 records)** and **20% testing (1,407 records)** using `train_test_split` with `random_state=42` for reproducibility. All feature scaling was fit exclusively on the training set and applied to the test set to prevent data leakage.

### Results

| Metric | Logistic Regression | Random Forest |
|---|---|---|
| **Accuracy** | **78.68%** | 78.46% |
| **AUC-ROC** | **0.83** | 0.82 |
| Precision (No Churn) | 83% | 82% |
| Recall (No Churn) | 88% | 90% |
| F1-Score (No Churn) | 86% | 86% |
| Precision (Churn) | 62% | 63% |
| Recall (Churn) | 52% | 47% |
| F1-Score (Churn) | 56% | 54% |

**Selected Model: Logistic Regression** — marginally higher accuracy and AUC score.

> **Note on accuracy vs AUC:** With a 26.58% positive class (churners), a naive model predicting "no churn" always would achieve ~73% accuracy. Our model's **AUC-ROC of 0.83** confirms it genuinely distinguishes churners from non-churners 83% of the time — significantly above the 0.50 random baseline. Precision, recall, and F1 scores are reported above for full transparency.

### Known Limitations
- Model trained on a US-based proxy dataset; not yet validated on real Nigerian subscriber data
- No real-time data feed — currently a batch scoring tool
- Class imbalance (26%/74%) limits recall on the minority churn class
- No cost-of-intervention modelling included in current version

---

## Top Churn Drivers (Feature Importance)

| Rank | Feature | Importance Score |
|---|---|---|
| 1 | TotalCharges | 0.19 |
| 2 | MonthlyCharges | 0.17 |
| 3 | Tenure | 0.17 |
| 4 | InternetService_Fiber optic | 0.04 |
| 5 | PaymentMethod_Electronic check | 0.04 |

Financial variables and customer tenure dominate — customers who pay more and are newer carry the highest churn risk.

---

## Key EDA Findings

- **26.58%** overall churn rate across 7,032 customers
- **Month-to-month** contracts churn at **42.71%** vs only **2.85%** for two-year contracts
- **Fiber Optic** internet customers churn at **42%** vs DSL at **19%** and no internet at **7%**
- Churn is highest in the **first 10–20 months** of tenure and declines steadily thereafter
- Customers in the **$70–90 monthly charge band** have the highest churn rate (~38%)

---

## Repository Contents

| File | Description |
|---|---|
| `Okereke Obaji - Customer Churn Prediction.ipynb` | Full Jupyter notebook — data cleaning, EDA, modelling, evaluation |
| `Customer Churn Prediction.pbix` | Power BI Desktop dashboard file |
| `3MTT Capstone Presentation Okereke Obaji Eze.pptx` | Final presentation slide deck |
| `telco_churn_cleaned.csv` | Cleaned dataset after preprocessing |
| `feature_importance.csv` | Top 10 features with importance scores |
| `model_predictions.csv` | Actual vs predicted values for test set |
| `churn_by_contract.csv` | Churn rate summary by contract type |
| `README.md` | This file |

---

## How to Run

1. Download the IBM Telco Churn dataset from [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
2. Place `WA_Fn-UseC_-Telco-Customer-Churn.csv` in the same directory as the notebook
3. Open `Okereke Obaji - Customer Churn Prediction.ipynb` in Jupyter Notebook or Google Colab
4. Run all cells sequentially (Runtime → Run All in Colab)
5. Open `Customer Churn Prediction.pbix` in Power BI Desktop to view the dashboard

**Dependencies:**
```
pandas, numpy, matplotlib, seaborn, scikit-learn
```
Install with: `pip install pandas numpy matplotlib seaborn scikit-learn`

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| Python 3 | Data cleaning, EDA, modelling |
| Pandas / NumPy | Data manipulation |
| Matplotlib / Seaborn | Visualisation |
| Scikit-learn | Machine learning models |
| Power BI Desktop | Interactive dashboard |
| Jupyter Notebook | Development environment |

---

## Programme Details

- **Programme:** 3MTT Nigeria (Three Million Technical Talent)
- **Cohort:** Cohort 3
- **Mentorship:** Wesonline Mentorship Programme
- **Mentor:** Abdulhafiz Ahmed
- **Track:** Advanced Data Analysis & Visualization

---

## Next Steps

1. **Q4 2025** — Deepen Python and machine learning skills through structured online courses (scikit-learn, model deployment, Flask/FastAPI)
2. **Q1 2026** — Rebuild this tool as a deployable web application with a user-facing dashboard, targeting Nigerian telecom operators
3. **Ongoing** — Validate model methodology against real Nigerian subscriber data when accessible; incorporate explainability layer (SHAP values) to improve retention team usability
4. **Career** — Pursue remote data analytics roles to gain real-world industry experience in applied data science

---

*Capstone project submitted as part of the 3MTT Nigeria Cohort 3 — Wesonline Mentorship Programme, Advanced Data Analysis & Visualization Track.*
