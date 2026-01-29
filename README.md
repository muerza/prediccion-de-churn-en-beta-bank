from pathlib import Path

readme_en = """# Beta Bank — Customer Churn Prediction 🏦📉

This project builds and evaluates **classification models** to predict whether a Beta Bank customer is likely to **leave the bank (churn)**.  
The goal is to help the business focus **retention efforts** on customers at higher risk.

---

## Goal 🎯

Predict the target variable:

- `Exited` → **1** if the customer left the bank, **0** otherwise.

---

## Dataset 📦

File used in the notebook: `Churn.csv` (expected in the project root).

Key features include:
- Customer profile: `Age`, `Gender`, `Geography`
- Account/relationship signals: `CreditScore`, `Tenure`, `Balance`, `NumOfProducts`, `HasCrCard`, `IsActiveMember`, `EstimatedSalary`

---

## What I did 🧩

### 1) Data prep & feature engineering
- Handled missing values in `Tenure` using:
  - **Median imputation**
  - A missing flag feature: `TenureWasMissing`
- Applied **one-hot encoding** to categorical features:
  - `Geography`, `Gender` (with `drop_first=True`)
- Scaled continuous features using `StandardScaler`:
  - `CreditScore`, `Balance`, `EstimatedSalary`

### 2) Train/validation split
- Split: **75% train / 25% validation** (`random_state = 54321`)

### 3) Class imbalance handling
The dataset is imbalanced (about **20.37% churn**).  
To help the model learn the minority class, I used **upsampling** on the training set (repeat factor = **3**).

### 4) Models evaluated
- **DecisionTreeClassifier (baseline)** — simple starting point (no upsampling)
- **DecisionTreeClassifier (tuned)** — hyperparameter search for `min_samples_leaf` and `max_depth`
- **RandomForestClassifier (tuned)** — hyperparameter search for `n_estimators` and `max_depth`
- **LogisticRegression** — trained on upsampled data

---

## Metrics 🧪

Evaluation uses:
- **Recall**, **Precision**, **F1**
- **ROC-AUC**
- **Average Precision (PR curve area)**
- Confusion matrix breakdown: TP / FP / TN / FN

---

## Results (validation set) 📊

| Model | Recall | F1 | PR AUC | ROC-AUC | Precision |
|---|---:|---:|---:|---:|---:|
| RandomForestClassifier | 0.6485 | **0.6212** | **0.6948** | **0.8718** | 0.5962 |
| DecisionTreeClassifier | **0.7259** | 0.5983 | 0.6723 | 0.8619 | 0.5088 |
| DecisionTree (baseline) | 0.4582 | 0.5177 | 0.4276 | 0.7465 | 0.5951 |
| LogisticRegression | 0.6004 | 0.4940 | 0.4463 | 0.7790 | 0.4196 |

✅ Best overall **F1**: **RandomForestClassifier (0.6212)**  
✅ Best **Recall** (catching churners): **DecisionTreeClassifier (0.7259)**

---

## How to run ▶️

1) Install dependencies:
```bash
pip install -r requirements.txt
