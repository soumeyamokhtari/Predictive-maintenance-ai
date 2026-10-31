# Cross-Domain Predictive Maintenance in Industrial IoT: Comparing Time- and Frequency-Domain Features Using Explainable XGBoost

## 🏆 MSc Dissertation Project — Grade: 81% (Distinction)

### 🔗 Live Interactive Dashboard
[👉 Click here to launch the Live Dashboard](https://predictive-maintenance-ai-c9hqs5elbyo72t7drefoqz.streamlit.app/)

---

## 📈 Executive Project Summary
This research investigates interpretable fault diagnosis for industrial sensor data. It develops an end-to-end Machine Learning framework following the **CRISP-DM** methodology, combining signal-processing features (**Fast Fourier Transform**) and physics-informed feature engineering. The framework is evaluated on two public datasets, one from a chemical/environmental setting and one from a mechanical setting.

### 📊 Model Performance
Using **XGBoost** models optimised via **GridSearchCV** and balanced via **SMOTE**, the following results were obtained on a held-out 20% test split:

* **Chemical Domain Expert Model:** **89.87% recall** | **89.31% F1-Score** (Evaluated on the Sensor Machine Failure Dataset)
* **Mechanical Domain Expert Model:** **80.88% recall** | **79.71% F1-Score** (Evaluated on the AI4I 2020 Predictive Maintenance Dataset)

*Note: AI4I 2020 is a synthetic benchmark dataset, so results may not transfer directly to real plant data.*

---

## 🔍 Explainable AI (XAI) & Feature Engineering Insights
**SHAP (SHapley Additive exPlanations)** was used to analyse which features the models relied on most when making predictions. SHAP describes model behaviour; it does not by itself establish the physical cause of a fault.

* **Chemical model:** `VOC` was the most influential feature. The engineered features `VOC_FFT` (frequency-domain) and `RP_std` (time-domain) also ranked highly.
* **Mechanical model:** `Tool_wear_min` was the most influential feature. The engineered features `Mechanical_Power`, `Temp_Delta_std` and `Tool_wear_min_FFT` also ranked highly.

---

## 🔬 Follow-up Analysis
After the dissertation, I ran a stricter evaluation on the AI4I dataset (repeated 5-fold cross-validation with SMOTE applied inside each fold, plus forward-chaining cross-validation):
* The physics-informed features (`Mechanical_Power`, `Temp_Delta`) gave the clear improvement: PR-AUC 0.81 → 0.86 under random cross-validation.
* Rolling time-domain and FFT features added no measurable benefit on top of the physics-informed features.
* Time-domain and frequency-domain features performed about the same.
* Under chronological evaluation, performance dropped for all feature sets. The test folds contain few failures, so these results are noisy.
* Model probabilities were calibrated (Platt scaling) because SMOTE shifts the class balance.

**Limitations:** AI4I is synthetic and its failure labels follow rule-based conditions, so these findings may not hold for real plants. Rows are not true consecutive time series for every sensor, so rolling-window features should be read as exploratory.

---

## 🛠️ Tech Stack
* **Language:** Python 3.x
* **Machine Learning:** XGBoost, Scikit-learn, SMOTE (Imbalanced-learn)
* **Explainable AI:** SHAP
* **Signal Processing:** Fast Fourier Transform (FFT), SciPy
* **Data Engineering:** Pandas, NumPy
* **Optimisation & Visualisation:** GridSearchCV, Streamlit Cloud

---

## 💻 Repository Contents
* [`Predictive_Maintenance.ipynb`](./Predictive_Maintenance.ipynb): the dissertation notebook (pipelines, evaluation metrics and SHAP visualisations).
* `app.py`: the Streamlit dashboard.

---

## 🚀 How to Run Locally

1. Clone this repository:
```bash
git clone https://github.com/soumeyamokhtari/Predictive-maintenance-ai.git
cd Predictive-maintenance-ai
```

2. Install the dependencies:
```bash
pip install -r requirements.txt
```

3. Launch the dashboard:
```bash
streamlit run app.py
```
