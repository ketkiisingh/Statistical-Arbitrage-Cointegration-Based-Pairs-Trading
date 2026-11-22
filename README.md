# Statistical Arbitrage: Cointegration-Based Pairs Trading

## Research Overview

This project investigates the statistical foundations and practical limitations of cointegration-based statistical arbitrage in US equity markets.

The research combines time-series econometrics, hypothesis testing, mean-reversion analysis, and transaction-cost-aware backtesting to evaluate whether economically related stock pairs exhibit sufficiently stable relationships to support a pairs-trading strategy.

The project emphasizes statistical validity, multiple-testing correction, realistic portfolio accounting, and transparent reporting of negative results.

## Research Question

**Can economically related US equity pairs exhibit statistically robust cointegration and generate profitable mean-reversion trading opportunities after transaction costs?**

## Methodology

### 1. Stationarity Testing

Augmented Dickey–Fuller (ADF) tests were used to investigate the stationarity properties of equity log prices and log returns.

This preliminary analysis informed the subsequent cointegration testing framework.

### 2. Cointegration Screening

Eight economically related stock pairs were evaluated using the Engle–Granger two-step cointegration test.

| Pair | Companies |
|---|---|
| V–MA | Visa – Mastercard |
| XOM–CVX | ExxonMobil – Chevron |
| BAC–C | Bank of America – Citigroup |
| JPM–WFC | JPMorgan Chase – Wells Fargo |
| BAC–WFC | Bank of America – Wells Fargo |
| WFC–C | Wells Fargo – Citigroup |
| JPM–C | JPMorgan Chase – Citigroup |
| JPM–BAC | JPMorgan Chase – Bank of America |

### 3. Multiple-Testing Correction

Because eight hypotheses were tested, the Benjamini–Hochberg false discovery rate (FDR) procedure was applied at the 5% significance level.

**Result: No pair remained statistically significant after FDR correction.**

The strongest exploratory candidate was Visa–Mastercard:

| Statistic | Value |
|---|---:|
| Raw Engle–Granger p-value | 0.013780 |
| FDR-adjusted p-value | 0.110241 |
| FDR significance threshold | 0.05 |

Although the unadjusted p-value suggested possible cointegration, the relationship did not survive multiple-testing correction.

The pair was therefore retained only for exploratory analysis, not as a statistically confirmed trading opportunity.

### 4. Spread Construction and Mean Reversion

For the Visa–Mastercard pair, a hedge-adjusted spread was estimated using ordinary least squares.

The fitted relationship produced:

| Parameter | Estimate |
|---|---:|
| Intercept | 0.333511 |
| Hedge ratio (β) | 0.858043 |
| AR(1) coefficient (φ) | 0.961188 |
| Estimated mean-reversion half-life | 17.51 trading days |

The estimated half-life suggested potentially measurable mean reversion.

However, rolling hedge-ratio diagnostics indicated parameter instability, raising concerns about the persistence of the relationship.

### 5. Trading Strategy

An exploratory mean-reversion strategy was evaluated using the Visa–Mastercard spread.

The strategy used:

- A 60-trading-day rolling z-score.
- Entry thresholds at +2 and −2 standard deviations.
- Exit when the spread z-score returned to zero.
- A maximum holding period of 45 trading days.
- A hedge ratio estimated from the earlier formation period.
- Next-session close execution assumptions.
- A 50% gross-exposure allocation.
- Transaction costs of 10 basis points per traded notional.

The strategy was evaluated over the 2024 calendar year.

### 6. Backtesting and Portfolio Accounting

An initial prototype was followed by a corrected holdings-based portfolio simulation.

The corrected implementation accounted for position holdings, portfolio equity, transaction costs, daily rebalancing, and end-of-period liquidation.

This distinction was important because simplified spread-return calculations did not reproduce the economics of the actual holdings-based strategy.

## Backtest Results

### Exploratory Visa–Mastercard Strategy — 2024

| Metric | Result |
|---|---:|
| Initial capital | $100,000.00 |
| Final equity before forced liquidation | $99,918.66 |
| Return before forced liquidation | −0.0813% |
| Trading and rebalancing fees | $707.44 |
| Additional liquidation cost | $49.96 |
| **Final equity after liquidation** | **$99,868.70** |
| **Final net return** | **−0.1313%** |

The corrected strategy produced a small negative net return after transaction costs and final liquidation.

The backtest illustrates how portfolio implementation assumptions and trading costs can materially affect the conclusions of a statistical arbitrage experiment.

## Key Research Findings

1. None of the eight tested pairs passed the 5% false-discovery-rate threshold.
2. Visa–Mastercard exhibited suggestive unadjusted cointegration evidence but failed the multiple-testing correction.
3. Estimated mean reversion did not establish that the relationship was stable enough for reliable trading.
4. Holdings-based accounting produced less favorable results than the initial simplified prototype.
5. Transaction costs and end-of-period liquidation were important to the final performance calculation.

## Limitations

- The Visa–Mastercard strategy was exploratory because the pair failed FDR-adjusted significance testing.
- Rolling hedge-ratio instability raised concerns about parameter robustness.
- Adjusted closing prices served as execution proxies rather than actual executable market quotes.
- Transaction-cost modelling was simplified; financing, borrow fees, market impact, and some spread-related costs were not fully represented.
- Portfolio exposure was not perfectly dollar-neutral.
- The 2024 validation period was not a pristine, fully untouched holdout.
- No independent 2025–2026 out-of-sample evaluation was completed.
- Results should not be interpreted as evidence of a deployable or consistently profitable trading strategy.

## Research Conclusion

This study finds that economically plausible equity relationships do not necessarily provide statistically robust or economically profitable arbitrage opportunities.

Although Visa–Mastercard displayed preliminary evidence of mean reversion, its cointegration result did not survive multiple-testing correction, and the corrected holdings-based backtest produced a negative net return.

The project demonstrates the importance of distinguishing statistical evidence from trading profitability, correcting for multiple hypothesis testing, evaluating parameter stability, and incorporating realistic portfolio accounting.

**The central contribution is a reproducible research process, not a claim of profitable statistical arbitrage.**

## Tools and Technologies

Python, NumPy, Pandas, statsmodels, Matplotlib, Jupyter Notebook, statistical hypothesis testing, cointegration analysis, and portfolio backtesting.

## Reproducibility

The research notebook should be executed sequentially, from data preparation and stationarity testing through cointegration screening, multiple-testing correction, spread diagnostics, strategy construction, and corrected holdings-based backtesting.

The final results correspond to the holdings-based implementation with forced year-end liquidation.

## Disclaimer

This project is an educational and exploratory quantitative research study. It does not constitute investment advice or demonstrate a production-ready trading strategy.
