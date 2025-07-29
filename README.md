# 🕵️‍♂️ Fraudulent Transaction Detection using Machine Learning

This project is a Machine Learning solution for detecting fraudulent financial transactions. It is based on a real-world inspired dataset and aims to help financial institutions proactively identify and prevent fraud.

## 📌 Problem Statement

The goal is to build a classification model that predicts whether a transaction is fraudulent (`isFraud = 1`) or not (`isFraud = 0`). The model is trained using transaction-related features such as amount, type, balances before/after the transaction, and more.

## 📂 Dataset Overview

- **Rows**: 6.3 million transactions
- **Columns**: 11 features
- **Target**: `isFraud` (1 = fraud, 0 = genuine)
- **Types of Transactions**: `PAYMENT`, `TRANSFER`, `CASH_OUT`, `CASH_IN`, `DEBIT`
- **Source**: Provided as part of a data science assignment (not publicly available)

### 🗂 Key Features

- `type`: Type of transaction
- `amount`: Transaction amount
- `oldbalanceOrg` / `newbalanceOrig`: Sender’s balance before/after
- `oldbalanceDest` / `newbalanceDest`: Recipient’s balance before/after
- `isFraud`: Label for fraud
- `isFlaggedFraud`: Flag if transaction exceeds a threshold (₹200,000+)

---

## 🧹 Step 1: Data Cleaning

- Removed duplicates
- Checked and handled outliers using boxplots and IQR
- Assessed multicollinearity using correlation heatmaps
- Dropped non-predictive columns (e.g., account IDs)

---

## 📊 Step 2: Exploratory Data Analysis (EDA)

- Analyzed class imbalance (fraud ≈ 0.1%)
- Fraud occurs almost exclusively in `TRANSFER` and `CASH_OUT`
- Most fraudulent transactions completely drain the sender’s balance

---

## 🏗 Step 3: Feature Engineering

- Created `balanceDiff` = difference in sender's balance
- Added binary feature `isMerchant` from recipient ID
- One-hot encoded `type` column

---

## 🤖 Step 4: Model Development

- Model used: `RandomForestClassifier`
- Train-test split: 70-30 with stratification
- Metrics used:
  - Precision, Recall, F1-Score
  - Confusion Matrix
  - ROC AUC Score

---

## 🔍 Step 5: Insights

### Key predictors of fraud:
- Transaction amount
- Old and new balances
- Transaction type
- Balance difference

### Do they make sense?
Yes! Fraudsters often:
- Transfer large amounts
- Drain accounts (zero out sender balance)
- Use `TRANSFER` or `CASH_OUT`

---

## 🛡️ Prevention Recommendations

- Monitor `TRANSFER` and `CASH_OUT` transactions in real time
- Flag multiple large transactions in short time windows
- Block accounts with rapid balance drops
- Introduce AI-driven rules for dynamic fraud detection thresholds

---

## 📉 Post-Implementation Evaluation

- Track drop in fraud rate
- Analyze reduction in false positives
- Use A/B testing with intervention/control groups
- Monitor transaction approval times and complaint rates

---

## 🚀 How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Run Jupyter Notebook
jupyter notebook Updated_Fraud_Detection_Assignment.ipynb
