# ML Drift Monitor

A production-style machine learning monitoring service to detect **data drift** and **prediction drift** in deployed ML systems.

This project focuses on **operating ML models in production**, not training them.

---

## 🚀 Overview

Machine learning models often fail silently when real-world data changes over time.  
The ML Drift Monitor helps identify when such changes occur by comparing **baseline distributions** with **live inference data**.

The system is designed to flag potential degradation early, enabling investigation or retraining before performance drops significantly.

---

## 🧠 What This Project Does

- Monitors incoming inference data in batches
- Compares live data against a reference (baseline) distribution
- Detects statistically significant drift
- Flags drift severity based on configurable thresholds
- Exposes monitoring results via a REST API

The project is **model-agnostic** and can be attached to any inference service.

---

## 🔍 Types of Drift Detected

### 1. Data Drift (Input Drift)
Detects changes in input feature distributions over time.

Examples:
- Text length distribution changes
- Feature value ranges shift
- Language or sentiment usage evolves

---

### 2. Prediction Drift (Output Drift)
Detects changes in model output distributions even if inputs appear similar.

Examples:
- Sudden increase in negative predictions
- Confidence scores becoming unstable

Prediction drift is often an early signal of model degradation.

---

## 🏗️ High-Level Architecture

1. **Baseline Data**
   - Historical or training-time data
   - Represents expected behavior

2. **Live Inference Data**
   - Collected during model inference
   - Processed in time-based or batch windows

3. **Drift Detection**
   - Statistical comparison between baseline and live data

4. **Alerting**
   - Drift scores categorized as low, medium, or high

---

## 📦 Tech Stack

- Python
- FastAPI
- Pandas, NumPy
- Statistical distance metrics
- Structured logging

---

## 📁 Project Structure

```text
ml-drift-monitor/
├── app/
│   ├── main.py          # API entry point
│   ├── drift.py         # Drift detection logic
│   ├── metrics.py       # Statistical distance functions
│   ├── schemas.py       # API request/response models
│   └── logger.py        # Logging setup
├── data/
│   ├── baseline.csv     # Reference distribution
│   └── live_sample.csv  # Example inference data
├── notebooks/
│   └── drift_analysis.ipynb
├── requirements.txt
└── README.md
