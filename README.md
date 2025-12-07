# A242 STTHK2113 DATA ANALYTICS (B)
- Assignment 3: Predictive Modelling 

# Project Details

Dataset link and credits: https://www.kaggle.com/datasets/ardikurniawan/hcvdat0

Objective: To determine blood eligibility based on age, sex, and other biological components.  

Process
- Data Cleaning: Input median, Clipping (Outliers), Log transformation (Skewness)
- Preprocessing: Standardization (Robust Scaling), encode categorical attributes (sec, category)
- Modelling Process:
  
  - Model Selected: Logistic Regression
  - Model Development:
      - Trained from 10:90 to 90:10
      - Graph of model performance containing evaluation metrics of Accuracy, Precision, Recall (Sensitivity), FQ-Score, ROC-AUC
   
Performance Evaluation:

- Top Three Ratios: 80:20, 70:30, 60:40 with Confusion Matrix, Sensitivity and Specificity

- Best Model Selected: 80:20 Split
