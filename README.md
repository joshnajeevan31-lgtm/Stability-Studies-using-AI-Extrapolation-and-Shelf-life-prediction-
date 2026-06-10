# Stability-Studies-using-AI-Extrapolation-and-Shelf-life-prediction-
An AI-driven predictive system that analyzes stability data to forecast degradation trends, extrapolate long-term storage behavior, and estimate product shelf life in accordance with ICH guidelines, reducing testing time and accelerating pharmaceutical development.

# 🧪 Shelf Life Prediction Software

> A kinetic regression-based impurity shelf life model built with Python and Streamlit — following ICH Q1E trend analysis guidelines.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-App-FF4B4B?logo=streamlit&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![scikit-learn](https://img.shields.io/badge/sklearn-LinearRegression-orange)

---

##What This Does

Stability studies track impurity growth over time. This app takes time-point impurity data, fits a linear regression model, and predicts **when the impurity will breach the specification limit** — giving you:

- A **formula-based shelf life** from the regression equation
- A **table-based shelf life** from step-wise extrapolation
- A **conservative shelf life** based on the 95% upper confidence interval
- A **publication-ready plot** with the regression line, extrapolation, CI band, and limit line

---

 [App Preview](Picture1.png) 

---



| Feature | Detail |
|---|---|
| 📥 Flexible input | Enter 2–100 time-point data pairs directly in the UI |
| ⏱️ Time unit selector | Supports Months, Days, or Hours |
| 🔢 Regression output | Slope, intercept, and R² displayed inline |
| 🔭 Extrapolation | Projects impurity trend up to a user-defined future range |
| 📐 95% Confidence Interval | Prediction interval (not just fit CI) — accounts for new observations |
| ⚠️ Conservative shelf life | Uses the CI upper bound to cross the spec limit — the safer, ICH-aligned estimate |
| 🟥 Beyond shelf life shading | Visual region on the plot marking post-expiry territory |
| 🟢🔴 Status table | Color-coded dataframe showing which future time points exceed the limit |

---

## 📊 How the Model Works

### Regression

OLS linear regression is fitted on the entered time vs. impurity data:

```python
from sklearn.linear_model import LinearRegression

lr = LinearRegression()
lr.fit(X_time, y_impurity)

slope     = lr.coef_[0]
intercept = lr.intercept_
```

### Formula-Based Shelf Life

The shelf life is solved algebraically from the regression equation:

```
shelf_life = (impurity_limit - intercept) / slope
```

### Prediction Interval (95% CI)

Unlike a confidence interval on the mean, this uses the **prediction interval** — the statistically correct approach for estimating when a *future* observation will cross the limit:

```
SE_pred = s * sqrt(1 + 1/n + (x_i - x̄)² / Sxx)
CI_upper = ŷ ± t(α/2, n-2) × SE_pred
```

This is consistent with the ICH Q1E recommendation to use the **one-sided upper confidence limit** for impurity growth shelf life estimation.

---

## 📈 Sample Output

```
Slope      :  0.002341 % / month
Intercept  :  0.031200 %
R²         :  0.9912

Shelf life (table)              =  24.00 months
Conservative Shelf Life (95% CI) =  21.50 months
```

---

## ▶️ Run Locally

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/shelf-life-predictor.git
cd shelf-life-predictor

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the app
streamlit run app.py
```

### requirements.txt

```
streamlit
numpy
pandas
scikit-learn
matplotlib
scipy
```

---

## 🌐 Live Demo

[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://YOUR-APP-URL.streamlit.app)

---

## 📂 File Structure

```
shelf-life-predictor/
│
├── app.py               # Full Streamlit app — input, model, CI, plot
├── requirements.txt
├── assets/
│   └── app_screenshot.png
└── README.md
```

---

## 🧾 Regulatory Context

This model is designed around:

- **ICH Q1A(R2)** — Stability Testing of New Drug Substances and Products
- **ICH Q1E** — Evaluation for Stability Data

Key alignment points:
- Uses **linear regression** as the primary trend model (ICH Q1E §2.1)
- Reports the **95% one-sided upper confidence limit** as the conservative shelf life — not just the point estimate
- Supports accelerated study time units (months, days, hours)

> **Disclaimer**: For research and educational use. Regulatory submissions require validated software and qualified person review.

---

## 👩‍🔬 Author

**Joshna** — Chemistry educator · AI/ML researcher · Cheminformatics  
MSc Organic Chemistry · BEd · BSc Chemistry & Biology

[LinkedIn](#) · [Portfolio](#) · [GitHub]([https://github.com/joshnajeevan31-lgtm])

---

## 📄 License

MIT — free to use and adapt with attribution.
