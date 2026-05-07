# Jane Street Cross-Sectional Signal Research

Cross-sectional signal modeling and statistical signal evaluation using the Jane Street Real-Time Market Data Kaggle dataset.

This project investigates short-horizon financial prediction using machine learning, robust forward-looking validation, and cross-sectional signal evaluation techniques.

---

# Project Overview

The objective of this research is to predict `responder_6` from anonymized market features provided in the Jane Street real-time forecasting dataset.

The workflow focuses on:

* strict forward-looking validation
* leakage-aware feature engineering
* weighted financial metrics
* LightGBM baseline modeling
* robustness diagnostics
* cross-sectional signal evaluation
* market-neutral ranking evaluation

The project was developed as a quantitative research pipeline inspired by standard cross-sectional quantitative research workflows.

---

# Dataset

Dataset source:

Jane Street Real-Time Market Data Forecasting Competition (Kaggle)

Dataset characteristics:

* ~25 million observations
* 90+ anonymized market features
* multiple financial instruments (`symbol_id`)
* intraday timestamps (`date_id`, `time_id`)
* weighted evaluation metric

The dataset itself is NOT included in this repository because of size and licensing constraints.

---

# Research Pipeline

The research workflow includes:

## 1. Data Diagnostics

* missing value analysis
* target distribution analysis
* temporal stability inspection
* feature sparsity analysis

---

## 2. Strict Time-Series Validation

Forward-looking train/validation split:

* training on earlier dates
* validation on future dates
* no random shuffling

This avoids temporal leakage and ensures realistic out-of-sample evaluation.

---

## 3. Baseline LightGBM Model

Main modeling choices:

* LightGBM regression
* weighted training
* weighted zero-mean R² metric
* missing values handled natively
* financial feature clipping
* feature sparsity filtering

Validation performance:

| Model             | Weighted R² |
| ----------------- | ----------- |
| Initial baseline  | ~0.0045     |
| Improved baseline | ~0.0086     |

---

## 4. Robustness Diagnostics

Several robustness checks were implemented:

* leakage checks
* harder out-of-sample validation
* shuffled-target test
* validation stability across dates
* overfitting diagnostics

Main findings:

* no evidence of major leakage
* evidence of statistically consistent out-of-sample ranking structure
* expected overfitting structure typical of financial ML

---

## 5. Lag Feature Experiment

Additional symbol-level lagged features were tested to evaluate temporal persistence effects.

Lag features were created using:

* grouped symbol history
* strictly past observations only
* multiple lag horizons

This experiment tested whether short-term feature memory improves predictive power.

---

## 6. Cross-Sectional Signal Construction

Model predictions were transformed into ranking-based cross-sectional signals.

The workflow includes:

* cross-sectional ranking
* Rank IC evaluation
* rolling Rank IC analysis
* signal decay analysis
* long-short ranking evaluation
* turnover estimation
* transaction-cost-adjusted diagnostics

---

# Key Results

## Predictive Signal

* Positive weighted R² out-of-sample
* Positive Rank IC
* Stable cross-sectional ranking structure

## Signal Diagnostics

Approximate validation results:

| Metric                   | Value  |
| ------------------------ | ------ |
| Mean Rank IC             | ~0.040 |
| Positive IC observations | ~59%   |
| Average turnover         | ~0.61  |

A simplified long-short portfolio simulation was used as a statistical ranking evaluation framework rather than a realistic tradable strategy.

Transaction costs were incorporated using a simplified fixed basis-point model in order to evaluate whether the ranking separation remained relatively stable after introducing basic trading frictions.

---

# Technologies Used

* Python
* Jupyter Notebook
* Pandas
* NumPy
* LightGBM
* Matplotlib
* Scikit-learn

---

# Repository Structure

```text
jane-street-cross-sectional-signal-research/
│
├── notebooks/
├── models/
├── artifacts/
├── figures/
├── README.md
├── requirements.txt
└── .gitignore
```
