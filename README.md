# Yield Curve Forecasting & Bond Portfolio Strategies

This project studies **yield curve dynamics** and designs **systematic bond trading strategies**
based on **machine learning forecasts of daily yield changes (Δy)**.

We decompose yield curve movements into **level, slope, and curvature**, forecast short-term yield
changes using multiple ML models, and evaluate their effectiveness through **out-of-sample backtesting**.

---

## 📌 Key Ideas

- Yield curve movements can be categorized into:
  - **Level**: parallel shifts
  - **Slope**: steepening / flattening
  - **Curvature**: butterfly movements
- Bond excess returns are primarily driven by **changes in yields**, captured through:
  - Duration
  - Convexity
- Accurate short-horizon yield forecasting enables **active fixed-income strategies**.

---

## 📊 Data

- **Instruments**: U.S. Treasury yields  
  - 5Y, 10Y, 20Y, 30Y (DGS5, DGS10, DGS20, DGS30)
- **Source**: FRED API
- **Sample period**:  
  - 1993-10-01 → 2023-04-11
- **Train / Test split**:
  - Test set: 2018-01-09 → 2023-04-11
- **Target**:  
  - Next-day yield change: Δy(t+1)
- **Features**:
  - Lagged yields (t−1 … t−6)
  - Extended lags (t−1 … t−60 for LSTM)
  - Market volatility (VIX)

---

## 🧠 Models Implemented

| Model | Description |
|------|------------|
| LSTM | Captures long-term temporal dependency in yield time series |
| SVM | Nonlinear regression on short lag structure |
| Neural Network | Feedforward NN baseline |
| Lasso | Linear model with L1 regularization and feature selection |
| Prophet | Trend-focused time series decomposition |

All models are evaluated using **MSE** and **MAPE** on an identical test set.

---

## 📈 Trading Strategies

Based on forecasted yield movements, we construct:

### 1. Level Strategies
- Increase duration when yields are expected to fall
- Decrease duration when yields are expected to rise

### 2. Slope Strategies
- Long bonds expected to outperform the curve
- Short bonds expected to underperform

### 3. Curvature (Butterfly) Strategies
- Long barbell / short bullet when curvature decreases
- Short barbell / long bullet when curvature increases

---

## 🔬 Backtesting & Metrics

Performance is evaluated using:

- Average return
- Cumulative return
- Sharpe ratio
- Sortino ratio
- Treynor ratio

---

## 🏆 Results Summary

### Model Forecast Accuracy (MAPE)

| Model | Performance |
|------|------------|
| **Lasso** | **~0.9% (best overall)** |
| LSTM | 2–4% |
| Neural Network | ~3–6% |
| SVM | Weak |
| Prophet | Poor short-term accuracy |

### Excess Return (Strategy Backtest)

| Model | Excess Return |
|------|--------------|
| Lasso | ~5% |
| LSTM | ~3.7% |
| NN | ~3.6% |
| SVM | ~2.3% |
| Prophet | High but unstable |

**Key Insight**:
- **Lasso** performs best for **short-horizon yield change prediction** and produces
  stable excess returns.
- **Prophet** captures long-term trends well but struggles with daily Δy prediction,
  leading to unstable signals.

---

## 🧾 Conclusion

- Yield curve dynamics can be effectively exploited using ML-based Δy forecasts.
- **Regularized linear models (Lasso)** outperform more complex models in this setting.
- Accurate short-term forecasting matters more than long-term trend fitting for
  fixed-income trading.

---

## 🚀 Future Improvements

- Incorporate macro variables (inflation, policy rates, volatility indices)
- Hyperparameter tuning and model ensembling
- Expanded bond universes and alternative backtesting schemes

---

## 👥 Authors

- Pei Zhu  
- Linglan Xu  
- Feiran Chen  
- Chengcheng Lu  
- Ruoyi Wang  
- Yitao Huang
