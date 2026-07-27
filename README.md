# Blood Donor Eligibility Prediction — HCV Dataset

**Course:** STTHK2113 Data Analytics (B)<br>
**Session:** 2024/2025 (A242)<br>
**Institution:** School of Computing, Universiti Utara Malaysia<br>
**Type:** Group Assignment 3 — Predictive Modelling Task<br>

---

## Overview

A binary classification project that predicts whether a patient is eligible to donate blood, built on the Hepatitis C Virus (HCV) dataset. The pipeline covers data cleaning, transformation, and Logistic Regression modelling, evaluated across nine train-test split ratios (10:90 to 90:10) to identify the most reliable configuration for a healthcare screening context.

**Dataset:** [HCV dataset (Kaggle)](https://www.kaggle.com/datasets/ardikurniawan/hcvdat0) — 615 records, 14 attributes covering demographic and biochemical patient data, spanning five original categories (Blood Donor, suspect Blood Donor, Hepatitis, Fibrosis, Cirrhosis).

---

## Tech Stack

- **Python** — Pandas, NumPy
- **scikit-learn** — LabelEncoder, RobustScaler, LogisticRegression, evaluation metrics
- **Matplotlib / Seaborn** — boxplots, histograms, performance graphs

---

## Repository Structure

    Data/                          # hcvdata.csv
    Preprocessing.py               # Data cleaning and transformation scripts
    Modelling.py                   # Logistic Regression training and evaluation
    Cleaned_Dataset.xlsx           # Output after cleaning
    Preprocessed_Dataset.xlsx      # Output after encoding and scaling

---

## Pipeline Stages

### 1. Data Cleaning
Missing values in ALB, ALP, ALT, CHOL, and PROT were imputed using the median. Outliers were handled with a clipping method, restricting values to the 1st and 99th percentiles rather than removing rows, since the dataset only holds 615 records. Six highly skewed features (CREA, BIL, GGT, ALT, AST, ALP) were log-transformed using log1p, while AST and BIL remained skewed even after transformation and were left untransformed to preserve clinical interpretability.

### 2. Data Transformation
The Sex column was label-encoded (f = 0, m = 1). The Category column was mapped into a binary Target: 0 for Blood Donor, and 1 for the remaining four categories (suspect Blood Donor, Hepatitis, Fibrosis, Cirrhosis), since safety guidelines exclude anyone with liver abnormalities or infectious disease risk from donating. Numerical features were standardised using RobustScaler for resilience to outliers and skew.

### 3. Model Development
Logistic Regression was trained and evaluated across nine train:test ratios (10:90 through 90:10), using Age, Sex, and nine biochemical markers as features. Accuracy, Precision, Recall, F1-Score, ROC-AUC, confusion matrices, sensitivity, and specificity were tracked for every split.

### 4. Evaluation & Best Model Selection
The 90:10 split scored perfectly across every metric but was rejected due to overfitting risk from its small test size. The 80:20, 70:30, and 60:40 splits were selected as the top three for offering a realistic balance of training and testing data.

---

## Results Summary

| Train:Test | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---|---|---|---|---|
| 80:20 | 0.9919 | 1.0000 | 0.9375 | 0.9677 | 1.0000 |
| 70:30 | 0.9784 | 1.0000 | 0.8400 | 0.9130 | 0.9965 |
| 60:40 | 0.9756 | 1.0000 | 0.8182 | 0.9000 | 0.9963 |

**Best model: 80:20 split.** It delivered the highest accuracy, recall, F1-score, and a perfect ROC-AUC, while holding perfect precision and specificity like the other two splits. Precision stayed at 1.0 across all top three ratios, meaning the model never misclassified a non-donor as eligible to donate, which is the priority in a blood-safety context.

---

## Findings

**No false positives across all top splits** — every split tested maintained perfect precision and specificity, so no ineligible patient was ever predicted as a safe donor.

**Recall trades off against test size** — sensitivity fell from 93.75% at 80:20 to 81.8% at 60:40, meaning smaller training sets increasingly missed real non-donor cases.

**Two features resisted transformation** — AST and BIL stayed skewed even after log1p, but RobustScaler's outlier resistance compensated during standardisation.

**90:10 looked perfect but wasn't trustworthy** — a small test set inflated every metric to 1.0, illustrating why raw scores alone can't determine the best split.

---

## Recommendations

- Test more sophisticated models such as Random Forest, SVM, or Gradient Boosting, particularly to better capture the AST and BIL relationships that remained skewed.
- Expand the dataset beyond 615 records to improve generalisability across more diverse patient profiles.
- Validate the model in a real clinical setting with continuous monitoring, since medical guidelines and data patterns can shift over time.
