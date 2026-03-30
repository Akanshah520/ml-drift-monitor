# Drift Forensics Lab — Acquisition Bias Study

## 1. Overview

This phase investigates the impact of acquisition bias on machine learning systems.

Acquisition bias occurs when the training data does not fully represent the true data distribution, often due to incomplete or skewed data collection processes.

The objective of this study is to understand how models behave when critical regions of the feature space are systematically underrepresented during training, while evaluation is performed on the full, unbiased distribution.

---

## 2. Objective

To analyze:

- How models respond to progressively increasing levels of acquisition bias
- Whether performance degradation occurs gradually or abruptly
- Whether early warning signals exist before accuracy declines
- Differences in behavior across model types

---

## 3. Experimental Design

### Dataset
- Breast Cancer Wisconsin dataset (scikit-learn)
- Binary classification problem
- Tabular feature space

### Bias Injection Strategy

A controlled bias is introduced by removing samples from the training data based on a high-impact feature:

- Feature: `worst perimeter`
- Method: Remove samples above a specified percentile threshold
- Test set remains unchanged

### Bias Levels

The following levels of bias were applied:

- 10% (remove top 10%)
- 20%
- 30%
- 40%
- 50%

This creates a progressive truncation of the feature distribution.

---

## 4. Models Evaluated

- Logistic Regression (linear model)
- Random Forest (tree-based ensemble)

These models were selected to represent contrasting inductive biases:

- Global linear decision boundary (Logistic Regression)
- Local partition-based decision structure (Random Forest)

---

## 5. Metrics

### Performance Metrics
- Accuracy
- ROC-AUC
- Log Loss

### Calibration and Stability Metrics
- Expected Calibration Error (ECE)
- Prediction confidence (mean and standard deviation)

---

## 6. Key Observations

### 6.1 Non-Linear Degradation

Model performance does not degrade linearly with increasing bias.

- Both models remain stable up to moderate bias levels (~20–30%)
- Beyond a threshold (~30–40%), degradation accelerates

---

### 6.2 Model-Specific Sensitivity

#### Logistic Regression
- Maintains high accuracy across all bias levels
- Shows gradual degradation
- Demonstrates robustness to missing feature regions

#### Random Forest
- Exhibits sharp performance decline beyond ~30–40% bias
- Log loss increases significantly before accuracy collapse
- Indicates sensitivity to missing regions in feature space

---

### 6.3 Early Warning Signals

Log loss increases before accuracy drops, particularly for Random Forest.

This suggests:

- The model becomes increasingly overconfident in incorrect predictions
- Calibration degrades before classification performance

This represents a **silent failure mode**.

---

### 6.4 Existence of a Tipping Point

A clear tipping point is observed:

- Below threshold: system appears stable
- Near threshold: instability begins
- Beyond threshold: rapid performance collapse

This indicates that model robustness has limits that are not visible through standard evaluation metrics alone.

---

## 7. Key Insight

Acquisition bias does not always produce immediate performance degradation.

Instead, it can:

- Preserve high accuracy
- Mask underlying instability
- Introduce blind spots in the learned decision space

This creates a false sense of model reliability.

---

## 8. Implications

- High accuracy does not guarantee robustness
- Calibration metrics are critical for early detection
- Tree-based models are more sensitive to distribution truncation
- Data coverage is as important as data quantity

---

## 9. Conclusion

This study demonstrates that:

- Machine learning systems can remain apparently stable under moderate acquisition bias
- Performance degradation often occurs abruptly rather than gradually
- Early indicators such as log loss and calibration error provide valuable signals before failure

Understanding these behaviors is essential for building reliable ML systems in real-world environments.

---

## 10. Next Steps

- Formalize early drift detection using calibration-based metrics
- Extend analysis to other forms of drift (preprocessing, label noise)
- Evaluate behavior across additional model classes
- Apply findings to more complex systems such as RAG pipelines

---

## 11. Reproducibility

- Fixed random seed
- Deterministic train-test split
- Controlled bias injection
- Consistent evaluation pipeline
