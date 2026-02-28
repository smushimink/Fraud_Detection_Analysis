
# Accounting Fraud Detection Pipeline

End-to-end fraud analytics pipeline combining:

* **Benford’s Law (digit analysis)**
* **Supervised classification (Logistic Regression + Decision Tree)**
* **Unsupervised anomaly detection (K-Means + Isolation Forest)**
* **Composite risk scoring + automated flagging**

Built in Python for forensic accounting, audit analytics, and financial crime detection.

---

## Overview

This project implements a full fraud detection workflow designed for transaction-level financial data.

The pipeline:

1. Cleans and engineers transaction features
2. Screens for numeric manipulation using Benford’s Law
3. Trains supervised models (if fraud labels are available)
4. Detects anomalies using unsupervised learning
5. Combines signals into a composite fraud risk score
6. Flags the top X% of high-risk transactions

Optimized for the Kaggle **Credit Card Fraud Dataset**, but adaptable to generic accounting datasets (GL transactions, invoices, AP/AR records).

---

## Tech Stack

* Python 3.11+
* pandas
* numpy
* scikit-learn
* matplotlib
* scipy

---

## 📂 Project Structure

```
fraud-detection-pipeline/
│
├── fraud_detection_pipeline.py
├── output/
│   ├── benford_comparison.png
│   ├── roc_curve.png
│   ├── confusion_matrix.png
│   ├── cluster_plot.png
│   └── flagged_transactions.csv
├── .gitignore
└── README.md
```

---

## Methodology

### 1️⃣ Benford’s Law Analysis

* Extract first digit of transaction amounts
* Compare observed vs expected digit frequencies
* Apply:

  * Chi-square goodness-of-fit test
  * Nigrini’s MAD statistic
* Flag digit-level deviations

Used as a screening tool for fabricated or manipulated numeric patterns.

---

### 2️⃣ Supervised Fraud Classification

If fraud labels exist:

* Logistic Regression (class-weight balanced)
* Decision Tree (interpretable rule extraction)

Metrics reported:

* Precision
* Recall
* F1-score
* ROC-AUC
* Confusion Matrix

Model selection based on highest ROC-AUC.

---

### 3️⃣ Unsupervised Anomaly Detection

* K-Means clustering (k chosen via silhouette score)
* Isolation Forest (top 2% anomalies by default)
* PCA visualization for cluster inspection

Captures structural outliers independent of labels.

---

### 4️⃣ Composite Risk Scoring

Risk score combines normalized:

* Benford deviation
* Isolation Forest anomaly score
* Absolute amount z-score
* Model fraud probability (if available)

Transactions in the top X% (default 2%) are flagged as high-risk.

---

## 📊 Example Results (Credit Card Fraud Dataset)

* Dataset size: 284,807 transactions
* Fraud rate: 0.17%

Logistic Regression:

* ROC-AUC ≈ 0.97
* Recall ≈ 88%
* Precision ≈ 6%

Isolation Forest:

* Flags top 2%
* Captures ~66% of fraud cases

Composite Risk Flagging:

* Top 2% flagged
* Captures ~80% of total fraud

---

## How to Run

### Option 1 — With local CSV

Place your dataset in the project folder:

```
creditcard.csv
```

Then run:

```bash
python fraud_detection_pipeline.py
```

Or specify a file:

```bash
python fraud_detection_pipeline.py --csv your_data.csv
```

Adjust risk threshold:

```bash
python fraud_detection_pipeline.py --risk-pct 0.05
```

---

### Option 2 — Auto-download Kaggle dataset

Install:

```bash
pip install kagglehub
```

Then run the script — dataset downloads automatically.

---

## 📈 Output Files

The pipeline generates:

* `benford_comparison.png`
* `roc_curve.png`
* `confusion_matrix.png`
* `cluster_plot.png`
* `flagged_transactions.csv`

The CSV includes:

* Original transaction data
* Fraud probability
* Anomaly score
* Composite risk score
* High-risk flag

---

## Applications

* Internal audit analytics
* Forensic accounting investigations
* Financial crime detection
* AML screening
* Compliance monitoring
* External audit transaction testing

---

## ⚠️ Important Notes

* Benford’s Law is most appropriate for naturally occurring accounting datasets.
* Fraud datasets are highly imbalanced; high recall often implies low precision.
* Threshold tuning should align with operational review capacity.

---

## Future Improvements

* Precision-recall curve optimization
* Cost-sensitive classification
* XGBoost / ensemble models
* Network fraud detection (graph-based methods)
* Real-time streaming integration

---

## Author

ZiYi (Violette) Hong
Econometrics | Accounting | Data Analytics | Fraud & Risk Modeling
