# Astronomy 101 (AE-0918) — Equinox

A semester of coursework spanning statistical modeling on real NASA
satellite data, a Kaggle competition, and hands-on astrophotography —
culminating in a final project that combines machine learning,
LaTeX report writing, and deep-sky image processing.

---

## 🌟 Final Project: Solar Flare Prediction & M31 Astrophotography

The capstone project, spanning three modules: theoretical astrophysics,
a machine learning pipeline for solar flare forecasting, and processed
astrophotography of the Andromeda Galaxy (M31).

**Key result:** Built and tuned five tree-based classifiers (Decision
Tree, Random Forest, AdaBoost, Gradient Boosting, XGBoost) to predict
M5+ solar flares from NASA SDO magnetogram data (SHARP parameters).
The final XGBoost model achieved **F1 = 0.967, PR-AUC = 0.993** on a
validation split — but evaluation on a genuinely held-out, temporally
later test period revealed a **near-total performance collapse
(ROC-AUC ≈ 0.50)**, traced to a real distribution shift: active
regions in the test period were systematically weaker across nearly
every energy/current feature, even among confirmed flares — plausibly
tied to the solar activity cycle. Diagnosing *why* a well-validated
model fails, rather than only reporting that it works, is the part of
this project I'm proudest of.

| | |
|---|---|
| <img src="final-project/figures/ROC_curves.png" style="height:300px; width:auto; display:block; margin:auto;"> | <img src="final-project/andromeda_final.png" style="height:300px; width:auto; display:block; margin:auto;"> |
| Model comparison (5 algorithms) | Final processed image of M31 |

**What's inside `final-project/`:**
- `document.pdf` — full write-up (theoretical derivations, ML pipeline, astrophotography workflow)
- `final-project.ipynb` — Colab notebook: EDA → imbalance handling → feature engineering → model tuning → evaluation
- `figures/` — key plots (correlation heatmap, boxplots, ROC comparison)
- `andromeda_final.png` — final M31 image, stacked (DeepSkyStacker) → calibrated & stretched (Siril) → denoised (GIMP)

**Tech stack:** Python, pandas, scikit-learn, XGBoost, imbalanced-learn, matplotlib/seaborn, LaTeX, DeepSkyStacker, Siril, GIMP

---

## 📊 Week 2: Predicting Stellar Luminosity

Built a Linear Regression model predicting a star's luminosity from
its temperature, radius, and absolute magnitude (2,000-star dataset).

- Split 80/20 train/test, fit `LinearRegression`, evaluated with MAE, MSE, and R².
- **Result: R² = 0.567** — the model captures the general trend (luminosity scaling with temperature and radius) but leaves meaningful scatter unexplained, consistent with luminosity's steep, non-linear dependence on temperature (∝T⁴) that a purely linear model can't fully capture.

- `week2/Equinox_Week_2.ipynb`

---

## 🌌 Week 3: Galaxy Classification Challenge

Classified 750 synthetic galaxies into Spiral, Elliptical, or Irregular
types from measured physical features (brightness, size, ellipticity,
concentration index, star formation rate, etc.), comparing KNN,
Gaussian Naive Bayes, and SVM.

| Model | Accuracy | Precision | Recall | F1 |
|---|---|---|---|---|
| KNN (k=3) | 0.92 | 0.92 | 0.92 | 0.92 |
| KNN (k=7) | 0.94 | 0.94 | 0.94 | 0.94 |
| Gaussian NB | 0.95 | 0.95 | 0.95 | 0.95 |
| **SVM** | **0.96** | **0.96** | **0.96** | **0.96** |

**Result:** SVM performed best across every metric. Confusion matrices
showed Spiral and Irregular galaxies were most often confused with
each other — both classes share overlapping structural features in
this dataset — while Elliptical galaxies were reliably distinguished.

- `week3/Equinox_Week_3.ipynb`

---

## 🏆 Week 4: Kaggle — Exoplanet Detection Challenge

Built a stacked ensemble (XGBoost + LightGBM + Random Forest) to
detect exoplanet transits from 9,000 labeled stellar observations
(27 features: stellar and orbital parameters), evaluated via 10-fold
stratified cross-validation.

- Addressed class imbalance (6,877 negative : 2,123 positive, ratio ≈ 3.24) via `scale_pos_weight`.
- Removed known label-leaking features (orbital/planetary parameters directly derived from the transit signal) before training.
- **Result: ensemble out-of-fold accuracy ≈ 1.00**, matching most of the leaderboard (score ties broken on later decimal places) — final leaderboard rank: **39th**.

- `week4/week4latest.ipynb`
- [Live Kaggle notebook →](https://www.kaggle.com/code/shanky3140/notebook5c7fa3c46e)

---

## Repository Structure

```
.
├── final-project/
│   ├── document.pdf
│   ├── final-project.ipynb
│   ├── figures/
│   └── andromeda_final.png
├── week2/
│   └── Equinox_Week_2.ipynb
├── week3/
│   └── Equinox_Week_3.ipynb
└── week4/
    └── week4latest.ipynb
```
