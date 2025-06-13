# 📊 ACF and PACF Explained

This document provides a detailed conceptual explanation of **Autocorrelation Function (ACF)** and **Partial Autocorrelation Function (PACF)**, which are fundamental in time series analysis.

---

## 🔁 Autocorrelation Function (ACF)

### 📌 Definition:
The **Autocorrelation Function (ACF)** measures how strongly a time series is correlated with its past values (lags). It captures both **direct and indirect** relationships.

### 🧠 Intuition:
Think of autocorrelation as answering:  
*"How much does the current value depend on values from previous time steps?"*

### 📐 Mathematical Formula:
Given a time series $X_t$, the autocorrelation at lag $k$ is:

$$
\rho_k = \frac{\sum_{t=1}^{N-k} (X_t - \bar{X})(X_{t+k} - \bar{X})}{\sum_{t=1}^{N} (X_t - \bar{X})^2}
$$

Where:
- $\bar{X}$: Mean of the time series  
- $N$: Length of the series  
- $k$: Lag value

### 🔎 Interpretation:
- Values range between $-1$ and $1$
- $\rho_k = 1$ → perfect positive correlation  
- $\rho_k = 0$ → no correlation  
- $\rho_k = -1$ → perfect negative correlation

### 📈 Usage:
- Identifying **seasonality** (e.g., repeating patterns at regular lags)
- Detecting **long-term dependencies**
- Determining the number of **MA (Moving Average)** terms in an ARIMA model

---

## 🔗 Partial Autocorrelation Function (PACF)

### 📌 Definition:
The **Partial Autocorrelation Function (PACF)** measures the **direct correlation** between a time series and its lagged version, removing the effects of the **intermediate lags**.

### 🧠 Intuition:
PACF answers:  
*"How much does the value at time $t$ depend directly on the value at time $t-k$, ignoring the influence of time steps $t-1$ to $t-(k-1)$?"*

### 📐 Mathematical Insight:
The PACF at lag $k$ is the coefficient $\phi_k$ in an autoregressive model of order $k$:

$$
X_t = \phi_1 X_{t-1} + \phi_2 X_{t-2} + \dots + \phi_k X_{t-k} + \epsilon_t
$$

PACF at lag $k$ is the estimated coefficient $\phi_k$ when regressing $X_t$ on the previous $k$ lags.

### 🔎 Interpretation:
- Shows how each lag contributes **independently** to the series.
- Sharp cutoff in PACF suggests the **order of AR (AutoRegressive)** terms.

---

## 🧠 ACF vs PACF Summary

| Feature              | ACF                              | PACF                              |
|----------------------|-----------------------------------|------------------------------------|
| Measures              | Total correlation (direct + indirect) | Direct correlation only             |
| Used for              | MA($q$) model identification         | AR($p$) model identification          |
| Shape                 | Tapers off or cuts off gradually   | Sharp cutoff for AR process         |
| Includes influence of | All previous lags                  | Only current lag (after conditioning) |

---

## 🔄 Practical Insight

In **ARIMA modeling**, you use:
- **ACF** to decide $q$ (MA order)
- **PACF** to decide $p$ (AR order)

For example:
- If ACF tails off and PACF cuts off after lag 2 → likely AR(2)
- If PACF tails off and ACF cuts off after lag 1 → likely MA(1)

---
