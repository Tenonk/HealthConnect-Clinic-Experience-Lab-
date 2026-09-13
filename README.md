# HealthConnect Clinic – Machine Learning Engineering

**AnalystLab Africa Experience Lab | Week 4 & Week 5**  
**Track:** Machine Learning Engineering  
**Project:** Improving Patient Appointment Attendance and Healthcare Support Using Data and AI

---

## 📌 Project Overview

HealthConnect Clinic is a fictional outpatient healthcare provider facing a high rate of **patient no-shows**. Missed appointments lead to wasted clinical capacity, longer waiting times, and increased administrative overhead.

**Central question:**
> How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?

As a **Machine Learning Engineer**, my role is to design a **reliable, reproducible, and production-oriented ML system** that predicts the likelihood of a patient missing a scheduled appointment (no-show prediction).

---

## 🎯 Objectives

### Week 4 – Problem Understanding & System Design
- [x] Understand the HealthConnect business problem
- [x] Review the appointment dataset and data dictionary
- [x] Define the ML problem and target variable
- [x] Specify system inputs and outputs
- [x] Design high-level system architecture
- [x] Define the end-to-end ML workflow
- [x] Identify key dependencies, assumptions, limitations, and risks
- [x] Produce a professional ML System Design Document + diagrams

### Week 5 – Data Exploration, Preprocessing & Baseline Modeling
- [x] Perform thorough Exploratory Data Analysis (EDA)
- [x] Clean and preprocess the data
- [x] Implement a **strict temporal train/test split**
- [x] Build a reproducible preprocessing pipeline (ColumnTransformer)
- [x] Train and evaluate three baseline models (no hyperparameter tuning)
- [x] Compare models using Accuracy, Precision, Recall, F1, ROC-AUC and PR-AUC
- [x] Analyze feature importance
- [x] Select the best untuned model
- [x] Package models and preprocessing artefacts

---

## 📁 Repository Structure

```text
healthconnect-ml-engineering/
├── data/
│   ├── raw/                          # Original immutable dataset
│   └── processed/                    # Cleaned & transformed data
│       ├── X_train_processed.csv
│       ├── X_test_processed.csv
│       ├── y_train_processed.csv
│       └── y_test_processed.csv
├── notebooks/
│   ├── 01_exploratory_data_analysis_EN.ipynb
│   ├── 02_preprocessing.ipynb
│   └── model.ipynb
├── models/
│   ├── column_transformer.pkl
│   ├── decision_tree.pkl
│   └── random_forest.pkl
├── image/
│   ├── UNIVARIATE/
│   ├── BIVARIATE/
│   ├── CORRELATION/
│   ├── EVALUATION/                  # Confusion matrices, ROC, PR curves
│   └── IMPORTANCE/                  # Feature importance & SHAP plots
├── docs/
│   ├── HealthConnect_ML_System_Design_Document_Week4.pdf
│   ├── Fiche_Pedagogique_HealthConnect_ML_Engineering_Week4.pdf
│   ├── Report_NoShow_Prediction_AnalystLAB.pdf   # Week 5 full report
│   └── diagrams/
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 📊 Data Resources

| Resource                             | Description                                |
| ------------------------------------ | ------------------------------------------ |
| `HealthConnect_Appointment_Data.csv` | Fictional & anonymised appointment records |
| `HealthConnect_Data_Dictionary`      | Variable definitions and notes             |

**Key variables used for no-show prediction:**
- `booking_lead_days` (strongest predictor)
- `previous_no_shows`, `previous_appointments`
- `distance_to_clinic_km`, `waiting_time_minutes`
- `age` / `age_group`, `gender`
- `reminder_sent` / `reminder_channel`
- `appointment_type`, `appointment_day`, `appointment_time`
- **Target:** `appointment_outcome` → binarized as **Attended (1)** vs **No-Show / Cancelled (0)**

---

## 🏗️ System Design (Week 4)

### High-Level Architecture

```text
Data Sources
    ↓
Data Ingestion & Validation
    ↓
Feature Engineering & Preprocessing
    ↓
Model Training Pipeline
    ↓
Model Registry & Versioning
    ↓
Inference / Scoring Service (batch)
    ↓
Downstream Consumers (dashboards, alerts, GenAI)
```

### Input → Output Contract

| **Inputs**                     | **Outputs**                                |
| ------------------------------ | ------------------------------------------ |
| patient demographics & history | `appointment_id`                           |
| appointment details & timing   | `no_show_probability` (0–1)                |
| reminder information           | `no_show_risk_label` (Low / Medium / High) |
| distance & waiting time        | `prediction_timestamp`                     |
|                                | `model_version`                            |

---

## 📈 Week 5 – Key Results

### Temporal Split
- **Train:** 2025-01-01 → 2026-03-13 (4,000 samples)
- **Test:**  2026-03-13 → 2026-06-30 (1,000 samples)

### Models Trained (default hyperparameters – no tuning)

| Model               | Accuracy | Precision | Recall | F1-Score | ROC-AUC | AP (PR) |
|---------------------|----------|-----------|--------|----------|---------|---------|
| Gradient Boosting   | 0.605    | 0.588     | 0.501  | 0.541    | **0.648** | **0.611** |
| Random Forest       | 0.606    | 0.585     | 0.527  | 0.554    | 0.630   | 0.583   |
| **Decision Tree**   | **0.611**| **0.593** | 0.523  | **0.555**| 0.631   | 0.569   |

### Selected Model (Week 5)
**Decision Tree** – best overall performance on classical classification metrics (Accuracy, Precision, F1) while remaining simple and interpretable.

### Most Important Features
1. `booking_lead_days` (dominant)
2. `distance_to_clinic_km`
3. `age` / `waiting_time_minutes`
4. `previous_no_shows` / `previous_appointments`

---

## 📄 Deliverables

### Week 4
| File | Description |
|------|-------------|
| [ML System Design Document](docs/HealthConnect_ML_System_Design_Document_Week4.pdf) | Full design document |
| Architecture, Workflow & I/O diagrams | System design visuals |
| Fiche Pédagogique (FR) | Pedagogical summary |

### Week 5
| File | Description |
|------|-------------|
| [Full Project Report](docs/Report_NoShow_Prediction_AnalystLAB.pdf) | Complete EDA + Preprocessing + Modeling report |
| 3 Notebooks | Exploration, Preprocessing, Modeling |
| Preprocessing pipeline | `column_transformer.pkl` |
| Trained models | `decision_tree.pkl`, `random_forest.pkl` |
| Processed datasets | 4 CSV files in `data/processed/` |
| Evaluation & Importance plots | All figures in `image/` |

---

## ⚙️ Tech Stack

- **Language:** Python 3.10+
- **Data:** pandas, numpy, seaborn, matplotlib
- **ML:** scikit-learn (Decision Tree, Random Forest, Gradient Boosting)
- **Preprocessing:** ColumnTransformer, OneHotEncoder, StandardScaler
- **Tracking / Versioning:** Git + GitHub
- **Artefacts:** joblib

---

## 🚀 Next Steps (Week 6+)

- Hyperparameter optimization (GridSearch / Optuna)
- Advanced feature engineering & interactions
- Probability calibration
- TimeSeriesSplit cross-validation
- Model packaging for batch inference
- Monitoring strategy & concept drift detection

---

## ⚠️ Key Assumptions & Risks

**Assumptions**
- Dataset is sufficiently representative for a prototype
- Historical features are available at prediction time
- Cancelled appointments can be grouped with No-Shows

**Main Risks**
| Risk                      | Mitigation                                      |
|---------------------------|-------------------------------------------------|
| Temporal data leakage     | Strict time-based train/test split              |
| Class imbalance           | Focus on Precision-Recall metrics               |
| Concept drift             | Monitoring + periodic retraining                |
| Over-reliance on predictions | Clear documentation + human-in-the-loop     |

---

## 📚 References & Resources

- AnalystLab Africa – Experience Lab (Week 4 & Week 5)
- HealthConnect Appointment Dataset & Data Dictionary
- HealthConnect Clinic Knowledge Base

---

## 👤 Author

**Machine Learning Engineering Junior**  
Tenon KONE  
Internship at **AnalystLAB**

---

## 📝 License & Notes

This project is part of the **AnalystLab Africa Experience Lab** internship programme.  
All data is **fictional and anonymised**. Do not treat results as real-world clinical recommendations.

---

*Last updated: Week 5 – Exploratory Analysis, Preprocessing & Baseline Modeling*
