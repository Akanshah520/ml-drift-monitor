# Drift Forensics Lab — Baseline

## 1. Overview

Machine learning systems are typically constructed using well-defined pipelines: data acquisition, preprocessing, model training, and evaluation. Each component may behave as expected in isolation. However, in practice, model performance often degrades over time.

This project investigates a central question:

If every component in the pipeline is functioning correctly, why does overall system performance still degrade?

The goal is to identify hidden sources of instability that are not immediately visible through standard evaluation.

---

## 2. Objective

The objective of this phase is to establish a clean, reproducible baseline representing a stable and well-behaved machine learning system.

This baseline serves as a reference point for:

- Measuring performance degradation
- Detecting early signs of drift
- Analyzing model behavior under controlled perturbations
- Isolating root causes of failure

---

## 3. Dataset

- Breast Cancer Wisconsin dataset (scikit-learn)
- Binary classification problem
- Tabular, interpretable features

This dataset is chosen for its balance between simplicity and realism, allowing controlled experimentation while maintaining meaningful structure.

---

## 4. Models

Two model classes are used to establish baseline behavior:

- Logistic Regression  
  - Interpretable, linear model  
  - Provides insight into feature relationships  

- Random Forest  
  - Nonlinear ensemble model  
  - Serves as a robustness and comparison benchmark  

---

## 5. Experimental Setup

- Train-test split: 80-20 (stratified)
- Fixed random seed for reproducibility
- StandardScaler fitted only on training data
- No data leakage between train and test

---

## 6. Metrics

### Performance Metrics
- Accuracy
- F1 Score
- ROC-AUC
- Log Loss

### Calibration Metrics
- Calibration curve
- Expected Calibration Error (ECE)

### Model Behavior
- Feature importance (Random Forest)
- Model coefficients (Logistic Regression)
- Prediction confidence statistics (mean, standard deviation)
- Confusion matrix

### Data Characteristics
- Feature distribution statistics (mean, standard deviation)
- Class distribution (train vs test)

---

## 7. Baseline Observations

- Logistic Regression achieves higher accuracy and lower log loss than Random Forest
- The dataset is highly separable with low inherent noise
- Calibration error (ECE) is low, indicating reliable probability estimates
- Class distributions are consistent between training and test sets
- Model behavior is stable and predictable

This confirms that the system is operating under ideal conditions.

---

## 8. Key Insight

Even in a stable baseline:

- Calibration is not perfect
- Minor distribution differences exist
- Model assumptions remain implicit

This highlights a critical point:

Model degradation is often not caused by implementation errors, but by violations of underlying assumptions.

---

## 9. Next Steps

The next phase introduces controlled perturbations to simulate real-world failure modes:

- Acquisition bias (sampling distortion)
- Preprocessing inconsistencies
- Label noise injection

Each perturbation will be applied independently to analyze:

- Sensitivity of models to specific drift types
- Early indicators of degradation
- Differences between linear and nonlinear model behavior

---

## 10. Reproducibility

- Fixed random seed
- Deterministic data split
- Consistent preprocessing pipeline
- Metrics and feature statistics stored for comparison

---

## 11. Project Scope

This project focuses on understanding failure mechanisms rather than optimizing performance.

The primary goal is to analyze how and why models degrade, even when the system appears correct.

---

## 12. Future Work

- Extend analysis to more complex datasets
- Study drift in deep learning models
- Apply findings to Retrieval-Augmented Generation (RAG) systems
- Develop strategies for early drift detection and mitigation
