# Portfolio VaR and Expected Shortfall Analysis

**Wang Chang**  
Year 3 Quantitative Finance Student  
The University of Hong Kong

A Python-based analysis of my current equity portfolio using Parametric, Historical and Monte Carlo methods to estimate five-day Value at Risk and Expected Shortfall.


## Project Overview

I developed this project to better understand the market risk of my current equity holdings. The project estimates the portfolio’s five-day Value at Risk (VaR) and Expected Shortfall (ES) using three different methods:

- Parametric method
- Historical simulation
- Monte Carlo simulation

The estimates are compared across 90%, 95% and 99% confidence levels to evaluate both the potential loss threshold and the severity of losses beyond that threshold.

## Portfolio

The analysis is based on a portfolio value of USD 5,000:

| Asset | Weight |
|---|---:|
| AVGO | 50% |
| QQQ | 25% |
| MRVL | 15% |
| TSLA | 10% |

This is a concentrated technology-oriented portfolio. QQQ also contains exposure to some of the individual holdings, creating additional overlapping exposure.

## Analysis Settings

- **Portfolio value:** USD 5,000
- **Historical lookback period:** 5 years
- **Risk horizon:** 5 trading days
- **Confidence levels:** 90%, 95% and 99%
- **Monte Carlo simulations:** 100,000
- **Market data:** Adjusted closing prices from Yahoo Finance

## Data Preparation

The data-cleaning notebook:

1. Downloads adjusted closing prices from Yahoo Finance
2. Checks and removes incomplete observations
3. Aligns all assets across common trading dates
4. Calculates daily logarithmic returns
5. Reviews the largest absolute return observations
6. Exports a common cleaned dataset for all three risk models

Using the same cleaned dataset ensures that the results from the three methods are comparable.

## Methodology

### Parametric Method

Five-day rolling portfolio returns are used to estimate the sample mean and standard deviation. VaR and ES are then calculated under the assumption that five-day portfolio returns follow a normal distribution.

### Historical Simulation

Historical VaR is estimated directly from the lower-tail percentiles of the observed five-day rolling return distribution. Historical ES is calculated as the average loss beyond each corresponding VaR threshold.

### Monte Carlo Simulation

The historical five-day mean and standard deviation are used to simulate 100,000 normally distributed five-day portfolio-return scenarios. VaR and ES are calculated from the lower tail of the simulated distribution.

## Results

| Confidence | Parametric VaR | Parametric ES | Historical VaR | Historical ES | Monte Carlo VaR* | Monte Carlo ES* |
|---:|---:|---:|---:|---:|---:|---:|
| 90% | $299.82 | $419.06 | $277.43 | $428.49 | ≈$299 | ≈$419 |
| 95% | $391.33 | $496.57 | $393.27 | $530.46 | ≈$392 | ≈$497 |
| 99% | $562.97 | $648.32 | $616.72 | $707.62 | ≈$563 | ≈$647 |

\*Monte Carlo estimates may vary slightly between runs because new random scenarios are generated each time.

## Key Findings

- Parametric and Monte Carlo results are very similar because both methods use the same normal-distribution assumption and estimated parameters.
- Historical simulation produces higher 99% VaR and ES estimates, indicating that the observed historical distribution contains more severe tail losses than the fitted normal distribution.
- Expected Shortfall is consistently higher than VaR because it measures the average loss after the VaR threshold has been exceeded.
- The largest estimated risk is the 99% Historical ES of approximately USD 708, or 14.2% of the portfolio value.

Based on my personal risk tolerance for this concentrated equity portfolio, the estimated five-day losses remain within my acceptable range. However, the results also highlight meaningful concentration and tail risk, particularly under the historical method.

## Repository Structure

```text
Portfolio_VaR_ES_Analysis/
├── Datacleaning_Preparation.ipynb
├── Parametric_Method.ipynb
├── Historical_Method.ipynb
├── Monte_Carlo_Simulation_Method.ipynb
├── cleaned_log_returns.csv
├── requirements.txt
└── README.md
