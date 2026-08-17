# Customer Churn & Retention Analytics

An end-to-end customer churn analytics project using machine learning to identify customers at risk of churn and translate predictions into actionable retention strategies.

## Overview

This project analyzes customer churn for a telecommunications provider using the IBM Telco Customer Churn dataset.

The analysis covers:

- Data cleaning and validation
- Exploratory Data Analysis (EDA)
- Predictive modeling
- Model comparison
- Business-oriented threshold optimization
- Model explainability
- Customer risk segmentation
- Retention strategy recommendations

The core objective is:

> **Identify customers at risk of churn and prioritize retention efforts based on predicted risk.**

---

##  Business Problem

Customer churn can negatively impact recurring revenue and customer lifetime value.

The project aims to answer:

1. Which customer segments have the highest churn?
2. Can machine learning predict customers likely to churn?
3. Which model performs best?
4. What classification threshold is appropriate for a retention-focused use case?
5. How can predicted churn probabilities be converted into actionable customer risk segments?

---

## 📊 Dataset

**IBM Telco Customer Churn Dataset**

| Attribute | Value |
|---|---:|
| Customers | 7,043 |
| Features | 21 |
| Churned Customers | 1,869 |
| Overall Churn Rate | 26.54% |
| Target | Churn |

The dataset contains customer demographics, tenure, contract information, subscribed services, payment methods, and billing information.

---

## Exploratory Data Analysis

Key churn patterns identified:

| Segment | Churn Rate |
|---|---:|
| Month-to-month contract | **42.71%** |
| One-year contract | 11.27% |
| Two-year contract | 2.83% |
| 0–6 months tenure | **52.94%** |
| 49–72 months tenure | 9.51% |
| Fiber optic | **41.89%** |
| DSL | 18.96% |
| Electronic check | **45.29%** |

### Key Insights

- Newer customers have substantially higher churn.
- Month-to-month customers show significantly higher churn than longer-term contract customers.
- Fiber-optic customers represent a high-churn segment.
- Electronic-check customers have substantially higher churn.
- Churned customers have higher median monthly charges than retained customers.

These findings were used to provide business context for the predictive modeling stage.

---

## 🤖 Predictive Modeling

Three classification models were trained and compared:

- Logistic Regression
- Random Forest
- XGBoost

### Model Performance

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| **Logistic Regression** | **80.6%** | 65.7% | **55.9%** | **60.4%** | **84.2%** |
| Random Forest | 78.2% | 61.4% | 48.1% | 54.0% | 81.9% |
| XGBoost | 80.5% | **66.8%** | 52.7% | 58.9% | 84.1% |

### Selected Model

**Logistic Regression**

It was selected as the working model because it achieved the strongest overall combination of ROC-AUC and F1-score while providing interpretable model coefficients.

---

##  Business-Oriented Threshold Optimization

The default classification threshold of 0.50 was evaluated against alternative thresholds because a retention program may prioritize identifying more potential churners.

| Threshold | Precision | Recall | F1-Score |
|---:|---:|---:|---:|
| **0.30** | 51.9% | **75.4%** | **61.5%** |
| 0.40 | 56.8% | 66.8% | 61.4% |
| 0.50 | 65.7% | 55.9% | 60.4% |
| 0.60 | 71.8% | 40.1% | 51.5% |
| 0.70 | 74.2% | 18.4% | 29.6% |

### Business Decision

A **0.30 probability threshold** was selected for the retention use case.

This increased recall from:

**55.9% → 75.4%**

while slightly improving F1-score:

**60.4% → 61.5%**

The trade-off is lower precision, meaning more customers may be flagged for retention outreach.

---

##  Model Explainability

Logistic Regression coefficients were used to identify features associated with higher or lower predicted churn.

### Higher Predicted Churn

| Feature | Coefficient |
|---|---:|
| Fiber optic internet | +0.634 |
| Month-to-month contract | +0.583 |
| Total Charges | +0.536 |
| Streaming Movies = Yes | +0.201 |
| Streaming TV = Yes | +0.200 |
| Electronic check | +0.198 |
| Online Security = No | +0.156 |
| Tech Support = No | +0.132 |

### Lower Predicted Churn

| Feature | Coefficient |
|---|---:|
| Tenure | **−1.258** |
| Two-year contract | −0.777 |
| DSL internet | −0.649 |
| Monthly Charges | −0.592 |

These coefficients represent model associations rather than causal effects.

---

##  Customer Risk Segmentation

Predicted churn probabilities were converted into three risk tiers.

| Risk Tier | Probability Range | Customers | Share |
|---|---|---:|---:|
| Low Risk | < 30% | 866 | 61.5% |
| Medium Risk | 30–60% | 334 | 23.7% |
| High Risk | ≥ 60% | 209 | 14.8% |

This segmentation provides a practical way to prioritize retention resources.

---

##  Retention Strategy

Based on the analysis, the following actions are recommended:

### 1. Prioritize Early-Tenure Customers
Strengthen onboarding and proactive engagement during the first 6–12 months.

### 2. Target Month-to-Month Customers
Test suitable incentives for customers to move toward longer-term contracts.

### 3. Investigate Fiber-Optic Churn
Review service quality, pricing, and customer experience within this segment.

### 4. Review Electronic-Check Customers
Investigate potential billing friction and encourage convenient automatic payment options where appropriate.

### 5. Prioritize High-Risk Customers
Use predicted churn probability to prioritize customers for retention outreach.

---

## 🛠️ Tech Stack

**Language**
- Python

**Libraries**
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn

**Techniques**
- Exploratory Data Analysis
- Data Cleaning
- Feature Scaling
- One-Hot Encoding
- Stratified Train-Test Split
- Logistic Regression
- Random Forest
- XGBoost
- Classification Threshold Optimization
- Confusion Matrix Analysis
- Model Explainability
- Risk Segmentation

---

## Repository Structure

```text
customer-churn-retention-analytics/
│
├── Customer_Churn_Analysis.ipynb
├── Customer_Churn_Prediction_Report.pdf
├── README.md
├── WA_Fn-UseC_-Telco-Customer-Churn.csv
