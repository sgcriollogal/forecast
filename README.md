# Forecasting Pipeline — Synthetic Data Example

This repository contains a **portfolio-ready** example of a forecasting pipeline built with Python.  
It demonstrates end‑to‑end steps on **synthetic data**: data generation, demand segmentation via clustering, and segment‑specific forecasting models (naive/ESM‑like for regular demand and **Croston** for intermittent demand).

> ✅ All data in this repo is synthetic and safe to share publicly.

---

## ✨ What you’ll find here

- **Synthetic time series generation** for thousands of products
- **Feature engineering**: total volume, sales frequency, ADI (Average Demand Interval), CV² (squared coefficient of variation)
- **Demand segmentation** using **K‑Means** on ADI and CV²
- **Forecasting**:
  - Regular segment → simple average (naive / ESM‑like simulation)
  - Intermittent segment → **Croston’s method** (smoothed demand / smoothed interval)
- Clean, tutorial‑style **notebook** with English comments

---

## 🧱 Repository structure

```
.
├── FULL_FORECAST_PIPELINE.ipynb   # Main tutorial notebook
├── README.md                      # You are here
├── requirements.txt               # Minimal dependencies
└── .gitignore                     # Ignore cache/checkpoints
```

> Tip: If you later add small sample CSVs, place them in a `data/` folder and keep them lightweight (< 10 MB).

---

## 🧪 Environment setup

> Works on Python **3.9+**. Create a virtual environment (recommended).

**Windows (PowerShell):**
```bash
python -m venv .venv
.\.venv\Scriptsctivate
pip install -r requirements.txt
```

**macOS/Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Launch Jupyter and open the notebook:
```bash
jupyter notebook FULL_FORECAST_PIPELINE.ipynb
```

---

## 🔬 Method overview

### Feature engineering
- **Total_Volume**: sum of units sold
- **Num_Periods_Sold**: number of periods with non‑zero sales
- **ADI**: average time gap (in months) between sales events
- **CV²**: (std / mean)² of demand size

### Segmentation (K‑Means)
We cluster products in the **(ADI, CV²)** space into two groups.  
The cluster with **more sales periods** is labeled **Regular**; the other is **Intermittent**.

### Forecasting
- **Regular**: uses the historical **mean** as a simple baseline (similar flavor to a basic Exponential Smoothing in stability).
- **Intermittent**: implements **Croston’s method**—exponential smoothing of **demand sizes** and **intervals** separately; forecast = smoothed_demand / smoothed_interval.

> This is intentionally simple and explainable for portfolio purposes. In production, you could upgrade to ETS/ARIMA/Prophet/LSTM or intermittent variants (SBA/TSB).

---

## 📈 Reproducing results

1. Open the notebook and run all cells sequentially.  
2. You’ll see:
   - Segment counts (Regular vs Intermittent)
   - Segment profiles (average ADI, CV², volume)
   - Forecast samples for both segments

---

## 🧩 Customization ideas

- Visualize clusters (scatter of **ADI vs CV²**, color by segment)
- Add accuracy metrics (MAE/RMSE/MAPE) using a train/test split
- Swap K‑Means for another clustering method (e.g., Gaussian Mixtures)
- Replace the naive forecast with ETS or state‑of‑the‑art intermittent models

---

## 📜 License

MIT — feel free to use and adapt this project with attribution.
