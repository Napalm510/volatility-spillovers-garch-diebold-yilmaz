# Volatility Transmission Between Western and Asian Equity Markets

Project for **Financial Econometrics** (MSc Quantitative Finance and Insurance, University of Turin, January 2026).

The project measures how volatility spills over between the **S&P 500, Euro Stoxx 50, Nikkei 225, Hang Seng and Nifty 50**, and how these links change over time. It uses a two-step approach: univariate GARCH models for each market, then **Diebold–Yilmaz connectedness** on a VAR of the estimated volatilities.

## Method

1. **Data:** daily closes from Yahoo Finance, converted to weekly log-returns (954 weeks). The weekly frequency removes the non-synchronous trading effects caused by time zones.
2. **Conditional volatility:** GARCH(1,1), GJR-GARCH(1,1) and EGARCH(1,1), each with Gaussian and Student-t innovations, giving six candidates per market. The best model is chosen by log-likelihood, AIC and BIC.
3. **VAR on volatilities** with a stability check and the Wold MA representation.
4. **Generalised FEVD** (Pesaran–Shin, order-invariant) gives the total connectedness index, the directional to/from spillovers and the net spillovers.
5. **Time variation:** a rolling VAR over a window of W = 200 weeks, with a horizon of H = 4.

## Findings

- All return series are negatively skewed and fat-tailed, which favours Student-t innovations and asymmetric specifications.
- **Total connectedness rises sharply in crises.** When it is high, diversification across regions works less well.
- On average the Western benchmarks are net transmitters, and the **S&P 500 is the main one**, especially during global stress. The Nikkei is close to neutral, while the **Hang Seng and the Nifty are net receivers**. This pattern becomes stronger at longer horizons.

## Files

| File | Content |
|---|---|
| `FinancialEconometrics.ipynb` | Full analysis (executed, outputs included) |
| `Report.pdf` | Project report (12 pages) |

## Running it

The data are downloaded at runtime with `yfinance`, so no local files are needed.

```bash
pip install numpy pandas matplotlib statsmodels arch yfinance
jupyter notebook FinancialEconometrics.ipynb
```
