# Quantitative Modeling and Time-Series Forecasting

A comparative study of **Time Series Forecasting** and **Fundamental (Intrinsic) Valuation** for Apple Inc. (AAPL), combining quantitative forecasting models — SARIMA and Facebook Prophet — with traditional DCF-based business valuation.

---

## Table of Contents

- [Problem Statement](#problem-statement)
- [Approach](#approach)
- [Dataset](#dataset)
- [Results](#results)
- [Visualizations](#visualizations)
- [Tools & Libraries](#tools--libraries)
- [Setup Instructions](#setup-instructions)
- [Project Structure](#project-structure)
- [Author](#author)

---

## Problem Statement

Stock price prediction is one of the most challenging problems in quantitative finance due to the non-linear, noisy, and non-stationary nature of financial time series. This project addresses two fundamental questions:

1. **Can historical price patterns alone (Time Series Analysis) reliably forecast Apple's stock price?**
2. **How does a data-driven forecast compare to a fundamentals-driven Intrinsic Valuation (DCF)?**

The goal is to forecast Apple's stock price using SARIMA and Prophet models and benchmark the outcome against a Discounted Cash Flow (DCF) valuation to arrive at a holistic investment insight: *Is AAPL overvalued or undervalued?*

---

## Approach

The project is divided into two parallel tracks:

### Track 1 — Time Series Forecasting

1. **Exploratory Data Analysis (EDA)**
   - Line plots, box plots, distribution plots, IQR analysis
   - Year-wise, month-wise, and day-of-week price breakdowns
   - Heatmap of feature correlations

2. **Stationarity Analysis**
   - Augmented Dickey-Fuller (ADF) test
   - First-order differencing to achieve stationarity
   - ACF and PACF plots to identify AR and MA orders

3. **Time Series Decomposition**
   - Decomposed into trend, seasonality, and residual components

4. **SARIMA Modelling**
   - Grid search over `(p, d, q) × (P, D, Q, s)` parameters
   - Selected best model via AIC criterion
   - Residual diagnostics: Q-Q plot, distribution plot, ACF of residuals

5. **Facebook Prophet Modelling**
   - Additive regression model with trend, weekly, and yearly seasonality
   - Evaluated on both train and test splits

6. **Evaluation Metrics**
   - Mean Squared Error (MSE)
   - Mean Absolute Percentage Error (MAPE)
   - R² Score

### Track 2 — Fundamental Analysis (Intrinsic Valuation)

- Collected 10-K filings and financial reports from Apple's Investor Relations page
- Estimated Beta via regression against market returns
- Projected revenue growth rates using historical financial data
- Built a Discounted Cash Flow (DCF) model to compute intrinsic value
- Compared intrinsic value against prevailing market price to conclude: **overvalued or undervalued**

---

## Dataset

| Source | Description |
|---|---|
| [Yahoo Finance](https://finance.yahoo.com/) | AAPL daily OHLCV data, 01-Apr-2012 to 31-Dec-2019, 2011 records |
| [Apple Investor Relations](https://investor.apple.com/investor-relations/default.aspx) | 10-K filings, financial statements for DCF model |

Features in `AAPL.csv`: `Date`, `Open`, `High`, `Low`, `Close`, `Adj Close`, `Volume`

---

## Results

### SARIMA

| Metric | Value |
|---|---|
| MSE | — *(see notebook)* |
| MAPE | — *(see notebook)* |
| R² Score | — *(see notebook)* |

> Detailed numerical results are available in `Quantitative Modeling and Time-Series Forecasting.ipynb`.

### Prophet

Prophet captured the long-term upward trend and yearly seasonality effectively, with competitive MAPE on the test set.

### Fundamental Valuation

Using DCF with Prof. Damodaran's framework, Apple's intrinsic value was computed and compared against the market price — yielding an **overvalued / undervalued** conclusion. *(See `Project Report.pdf` and Business Valuation CSVs for full details.)*

### Key Takeaway

Both approaches converged on a consistent directional outlook for AAPL, validating the use of Time Series Forecasting as a complementary tool alongside traditional fundamental analysis for investment decision-making.

---

## Visualizations

All plots are saved under the `Visualizations/` folder:

| Plot | Description |
|---|---|
| `Features Line Plots.png` | OHLCV feature trends over time |
| `Avg Stock Prices by Year,Month,day_of_week,quarter.png` | Seasonal patterns |
| `Decomposed Time Series.png` | Trend + seasonality + residual decomposition |
| `ACF Plot-Orignal Time Series.png` | Autocorrelation of original series |
| `ACF & PACF-(Differenced Time Series).png` | ACF/PACF after differencing |
| `Stationarity Check-Differenced by 1-Time Series.png` | Stationarity post-differencing |
| `Residual Analysis-SARIMA-Train Data.png` | SARIMA train residuals |
| `Distribution & ACF Plot -SARIMA-Test Data Residual.png` | SARIMA test residuals |
| `Forecasting -SARIMA.png` | SARIMA forecast vs actuals |
| `Prophet-Forecasting-Train Data.png` | Prophet fit on training data |
| `Prophet Forecasting-Test Data.png` | Prophet forecast on test data |
| `HeatMap.png` | Feature correlation heatmap |
| `QQ Plot-Normality Test.png` | Normality check on residuals |

---

## Tools & Libraries

| Tool / Library | Purpose |
|---|---|
| Python 3.6 | Core language |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Matplotlib / Seaborn | Visualization |
| Statsmodels | SARIMA modelling, ADF test, ACF/PACF |
| Scikit-learn | Evaluation metrics (MSE, R²) |
| SciPy | Statistical tests |
| fbprophet | Facebook Prophet forecasting |

---

## Setup Instructions

### Prerequisites

- Python 3.6+ (Python 3.6 recommended for fbprophet compatibility)
- pip or conda

### 1. Clone the Repository

```bash
git clone https://github.com/Anjaliydv2181/Quantitative-Modeling-and-Time-Series-Forecasting.git
cd Quantitative-Modeling-and-Time-Series-Forecasting
```

### 2. Create a Virtual Environment (recommended)

```bash
python -m venv venv
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn statsmodels scikit-learn scipy
pip install pystan==2.19.1.1
pip install fbprophet
```

> **Note:** `fbprophet` (now `prophet`) requires `pystan`. If you encounter installation issues, use:
> ```bash
> conda install -c conda-forge prophet
> ```

### 4. Launch the Notebook

```bash
jupyter notebook "Quantitative Modeling and Time-Series Forecasting.ipynb"
```

### 5. Data

The dataset `AAPL.csv` is included in the repository. No additional download is needed for the time series analysis. For the business valuation, refer to the CSVs in the `Business Valuation/` folder.

---

## Project Structure

```
├── AAPL.csv                              # Apple stock price data (2012–2019)
├── Quantitative Modeling and Time-Series Forecasting.ipynb   # Main notebook
├── Project Report.pdf                    # Full project report
├── Business Valuation/
│   ├── Apple Beta Calculation.csv
│   ├── Apple Discounted Cash Flow Sheet.csv
│   └── Predicting growth rates.csv
├── Visualizations/                       # All generated plots
└── README.md
```

---

## Author

**Anjali Yadav**  
Indian Institute of Technology (IIT) Madras

---

*For questions or feedback, feel free to open an issue or reach out via GitHub.*
