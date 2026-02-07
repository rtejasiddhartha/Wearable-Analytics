# Wearable Health Analytics & Risk Monitoring

## Overview
This project builds an end-to-end **wearable health analytics and risk intelligence system** using real-world wearable sensor data. The goal is to transform raw, noisy wearable signals into **validated health indicators, longitudinal risk patterns, and interpretable machine-learning insights** that go beyond what typical consumer health apps provide.

Unlike snapshot-based fitness summaries, this project focuses on **temporal health behavior**, **data quality awareness**, and **risk escalation logic**, making it suitable for **remote patient monitoring (RPM)** and preventive health analytics.

---

## Key Objectives
- Convert raw wearable data into **analysis-ready datasets**
- Analyze **sleep, activity, and heart rate** independently and jointly
- Engineer **health risk features** with real-world data gaps
- Build a unified **health timeline** for longitudinal monitoring
- Apply **interpretable machine learning** for health risk classification
- Evaluate (and critically validate) the role of **ECG data**

---

## Data Characteristics
- Multi-year wearable data (Apple Watch, iPhone, Mi Band, Amazfit)
- Mixed granularity (minute-level, interval-level, daily summaries)
- Realistic missing days, partial recordings, and device sync issues
- Combination of **real wearable data** and **controlled synthetic ECG scenarios**

---

## Notebook Breakdown

### 1. `sleep_analytics.ipynb`
**Purpose:** Sleep quality analytics and risk feature generation  
**Key Logic:**
- Nightly sleep aggregation
- Sleep efficiency, stage composition, fragmentation
- Extreme sleep detection (very low / very high)
- Sleep quality flags (poor, fragmented, low REM/deep)
- Stage availability & data reliability checks

**Outputs:**
- `nightly_sleep_full`
- Sleep risk features for downstream modeling

---

### 2. `steps_analytics.ipynb`
**Purpose:** Activity behavior analysis with realism constraints  
**Key Logic:**
- Interval-level step processing
- Steps-per-minute (SPM) validation
- Detection of impossible cadence bursts
- Daily step aggregation
- Activity risk flags (low activity, false spikes)

**Outputs:**
- `daily_steps`
- Activity reliability & risk features

---

### 3. `heart_rate_analytics.ipynb`
**Purpose:** Cardiovascular signal analytics  
**Key Logic:**
- Daily average, min, max heart rate
- Heart rate variability (HR std)
- Elevated / low HR minutes
- HR variability risk indicators
- HR data availability flags

**Outputs:**
- `daily_hr`
- HR risk and variability features

---

### 4. `workouts_analytics.ipynb`
**Purpose:** Supplemental activity context  
**Key Logic:**
- Workout duration & type analysis
- Source device validation
- Used as contextual support, not primary risk driver

**Note:**  
Workout data is intentionally **not over-weighted**, reflecting real-world sparsity.

---

### 5. `health_integration.ipynb` (Core Intelligence Layer)
**Purpose:** Unified health timeline & ML risk modeling  
**Key Logic:**
- Merge sleep, activity, and HR on date
- Graceful handling of partial data days
- Feature availability awareness (no forced imputation)
- Risk evidence computation:
  - Sleep risk evidence
  - Activity risk evidence
  - HR risk evidence
- Risk scoring & state classification:
  - Stable / Mild Risk / Elevated Risk
- Temporal features:
  - Risk streaks
  - Escalation flags
  - Early warning signals

**Machine Learning:**
- Logistic Regression (interpretable by design)
- Binary elevated risk classification
- ROC-AUC ≈ **0.96**
- Feature importance analysis (coefficients)

**Outputs:**
- `health_timeline`
- Final health risk state per day

---

### 6. `ecg_event_analysis.ipynb`
**Purpose:** ECG validation (not prediction)  
**Key Logic:**
- Integration of synthetic ECG risk events
- Scenario-based ECG stress periods
- Comparison against AI-detected risk days

**Key Finding:**
> ECG data **reinforced existing AI-detected risk** but did not introduce new independent risk signals.

This validates the model’s robustness and avoids artificial performance inflation.

---

## Why This Project Is Different from Typical Health Apps
- Consumer apps focus on **daily summaries**  
- This system focuses on **longitudinal risk trajectories**
- Explicit handling of **missing and unreliable data**
- Transparent, interpretable ML (not black-box scoring)
- Clear separation between **signal detection** and **clinical validation**
- Designed with **preventive monitoring**, not fitness gamification

---

## Tech Stack
- **Python**
  - Pandas, NumPy
  - Scikit-learn
- **Machine Learning**
  - Logistic Regression
  - Feature importance analysis
- **Analytics**
  - Exploratory Data Analysis (EDA)
  - Statistical validation
- **Data Handling**
  - Excel-based ingestion
  - Wearable XML exports
---

## Current Project Status
✅ Data engineering & validation  
✅ Sleep, activity, HR analytics  
✅ Feature engineering  
✅ Unified health timeline  
✅ Machine learning & evaluation  
✅ ECG validation analysis  

## Disclaimer
This project is **analytical and educational**, not a medical diagnostic system.  
Insights are intended to demonstrate data analytics and ML workflows using wearable health data.

---

## 👤 Author

**R. Teja Siddhartha**

- 💼 LinkedIn: https://linkedin.com/in/rtejasiddhartha  
- 💻 GitHub: https://github.com/rtejasiddhartha  
- 📧 Email: rtejasiddhartha18@gmail.com  

---

