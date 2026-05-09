# Jane Street Cross-Sectional Alpha Signal Research

This project started as a predictive modeling task based on the Jane Street real-time forecasting competition and was progressively extended into a research-oriented cross-sectional signal evaluation framework.

The objective was initially to predict `responder_6` using machine-learning models under strict forward-looking validation, then evaluate whether the resulting predictions formed statistically meaningful cross-sectional ranking signals.

The workflow includes predictive modeling, robustness diagnostics, Rank IC analysis, signal decay evaluation, turnover analysis, and simplified market-neutral ranking diagnostics on anonymized financial market data.

---

# Project Overview

The project initially started as a predictive modeling task aligned with the Jane Street forecasting competition objective: predicting `responder_6` from anonymized market features.

It was progressively extended into a research-oriented signal evaluation framework designed to analyze whether model predictions exhibit stable cross-sectional ranking structure across time.

The workflow focuses on:

* strict forward-looking validation
* leakage-aware feature engineering
* weighted financial metrics
* LightGBM baseline modeling
* robustness diagnostics
* cross-sectional ranking evaluation
* signal persistence analysis
* simplified market-neutral ranking diagnostics

The project emphasizes methodological signal evaluation techniques commonly used in quantitative research, including Rank IC analysis, signal decay evaluation, turnover diagnostics, and portfolio-level ranking analysis.

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

Because the dataset is fully anonymized, the project focuses on statistical signal structure rather than direct economic interpretation of the predictive features.

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

The improvement mainly resulted from methodological corrections involving temporal sampling design, leakage control, feature filtering, and validation robustness rather than model complexity alone.

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
* statistically positive out-of-sample ranking structure across validation periods
* expected overfitting behavior typical of low signal-to-noise financial ML problems

---

## 5. Lag Feature Experiment

Additional symbol-level lagged features were tested to evaluate temporal persistence effects.

Lag features were created using:

* grouped symbol history
* strictly past observations only
* multiple lag horizons

This experiment evaluated whether short-term feature memory improves predictive structure.

---

## 6. Cross-Sectional Signal Construction

Model predictions were transformed into ranking-based cross-sectional signals.

The workflow includes:

* cross-sectional ranking
* Rank IC evaluation
* rolling Rank IC analysis
* signal decay analysis
* simplified long-short ranking diagnostics
* turnover estimation
* transaction-cost-adjusted diagnostics

The objective of this stage is not to claim deployable alpha generation, but to evaluate whether predictive model outputs form statistically stable ranking structure under forward-looking validation.

---

# Key Results

## Predictive Signal

* Positive weighted R² out-of-sample
* Positive Rank IC
* Moderately stable cross-sectional ranking structure across validation periods

## Signal Diagnostics

Approximate validation results:

| Metric                   | Value  |
| ------------------------ | ------ |
| Mean Rank IC             | ~0.040 |
| Positive IC observations | ~59%   |
| Average turnover         | ~0.61  |

A simplified market-neutral long-short framework was used as a ranking-based diagnostic tool rather than a realistic deployable trading strategy.

Transaction costs were incorporated using a simplified fixed basis-point model in order to evaluate whether ranking separation remained relatively stable after introducing basic trading frictions.

---
# Research Observations

Several experiments highlighted the difficulty of extracting stable predictive structure from noisy and non-stationary financial data.

For example:

* stronger regularization reduced overfitting but slightly lowered predictive performance
* symbol-level lag features did not materially improve out-of-sample ranking quality
* validation performance varied across time regimes
* harder out-of-sample splits significantly reduced weighted R²

These observations reinforced the importance of robust validation design and signal stability analysis rather than relying purely on model complexity.

# Research Limitations

This project uses a fully anonymized dataset, which prevents direct economic interpretation of the predictive structure.

The long-short framework is intentionally simplified and is used for ranking-based signal diagnostics rather than realistic execution modeling.

Transaction costs, liquidity effects, and market impact are modeled only through simplified assumptions and should not be interpreted as production-level trading estimates.

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
