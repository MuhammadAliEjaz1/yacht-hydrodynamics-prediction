# 🚢 Yacht Hydrodynamics — Residuary Resistance Prediction

> Regression | Feature Engineering | Optuna Tuning | SHAP Analysis  
> **Best Model: Gradient Boosting — R² = 99.8% | MSE = 0.23**  
> 🥉 Bronze Medal on Kaggle

---

## 📋 Overview

Predicting the **residuary resistance** of sailing yachts is a core problem in naval architecture — it directly determines how much power a yacht needs to maintain speed. This project builds a machine learning regression pipeline on the **UCI Yacht Hydrodynamics Dataset**, going beyond baseline models with physics-informed feature engineering, Bayesian hyperparameter optimization (Optuna), and SHAP explainability.

---

## 📊 Results

| Model | R² | MSE | MAE |
|-------|----|-----|-----|
| **Gradient Boosting (Tuned) — Final** | **99.80%** | **0.23** | — |
| Gradient Boosting (default) | ~98% | — | — |
| Random Forest | ~97% | — | — |
| XGBoost (default) | ~96% | — | — |
| SVR (RBF) | ~93% | — | — |
| Ridge / Lasso / Linear Regression | ~75–80% | — | — |

---

## 🗂️ Dataset

**Source:** [UCI Yacht Hydrodynamics Dataset](https://archive.ics.uci.edu/ml/datasets/Yacht+Hydrodynamics) — 308 samples, 6 features, no missing values.

| Feature | Description |
|---------|-------------|
| `LongPos_COB` | Longitudinal position of center of buoyancy |
| `Prismatic_Coeff` | Prismatic coefficient |
| `Length_Disp_Ratio` | Length-displacement ratio |
| `Beam_Draught_Ratio` | Beam-draught ratio |
| `Length_Beam_Ratio` | Length-beam ratio |
| `Froude_Number` | Froude number (speed-to-length ratio) |
| `Residuary_Resist` | **TARGET** — Residuary resistance per unit weight |

---

## ⚙️ Project Pipeline

```
Load Data → EDA → Feature Engineering → Train/Test Split → 
Baseline Comparison → Optuna Tuning → Final Evaluation → SHAP Analysis
```

### Key Steps

- **EDA:** Feature distributions, correlation heatmap, Froude Number vs Resistance scatter (revealing the non-linear relationship)
- **Physics-informed feature engineering:** Added 6 interaction/polynomial features based on domain knowledge:
  - `Froude²`, `Froude³` — captures the known non-linear speed-resistance curve
  - `Froude × Prismatic_Coeff`, `Froude × Length_Disp_Ratio` — hull-speed interactions
  - `Prismatic × Length_Beam`, `LengthDisp × Beam_Draught` — hull geometry interactions
- **7-model baseline comparison:** Linear, Ridge, Lasso, SVR, Random Forest, Gradient Boosting, XGBoost
- **Optuna hyperparameter tuning:** 100-trial Bayesian optimization on Gradient Boosting with 5-fold CV
- **SHAP analysis:** Feature importance bar plot + beeswarm plot confirming Froude Number as dominant predictor

---

## 🔍 Key Findings

- **Froude Number is the dominant predictor** — both built-in feature importance and SHAP agree. This aligns with naval hydrodynamics theory where speed (expressed as Froude number) is the primary driver of wave-making resistance.
- **Polynomial Froude features (², ³) were critical** — they allow the model to capture the exponential resistance curve that appears at higher speeds.
- **Linear models plateau around 75–80% R²** — confirming the non-linearity in the data that tree-based models handle naturally.
- **Optuna tuning pushed Gradient Boosting from ~98% → 99.8% R²** — meaningful improvement over default parameters.

---

## 🏗️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-latest-orange?logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-latest-red)
![Optuna](https://img.shields.io/badge/Optuna-Bayesian%20Tuning-6C63FF)
![SHAP](https://img.shields.io/badge/SHAP-Explainability-FF6B6B)
![Pandas](https://img.shields.io/badge/Pandas-latest-150458?logo=pandas)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)

---

## 🚀 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/MuhammadAliEjaz1/yacht-hydrodynamics-prediction.git
   cd yacht-hydrodynamics-prediction
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Launch the notebook**
   ```bash
   jupyter notebook yacht-hydrodynamics-residuary-resistance-predict.ipynb
   ```

---

## 📁 Repository Structure

```
yacht-hydrodynamics-prediction/
├── yacht-hydrodynamics-residuary-resistance-predict.ipynb  # Main notebook
├── yacht_hydro.csv                                         # Dataset
├── requirements.txt                                        # Dependencies
└── README.md                                               # This file
```

---

## 📦 requirements.txt

```
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
optuna
shap
jupyter
```

---

## 👤 Author

**Muhammad Ali Ejaz**  
[![Kaggle](https://img.shields.io/badge/Kaggle-chaliejaz-blue?logo=kaggle)](https://www.kaggle.com/chaliejaz)  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-muhammad--ali--ejaz-0077B5?logo=linkedin)](https://linkedin.com/in/muhammad-ali-ejaz-855117341)

---

*If you found this project helpful, please ⭐ the repository!*
