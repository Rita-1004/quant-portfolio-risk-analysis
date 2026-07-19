# Quantitative Portfolio Optimization and Risk Management with Factor Analysis

## 1. Project Overview

This project develops a quantitative portfolio optimization and risk management framework to investigate whether systematic portfolio construction methods can improve risk-adjusted performance compared with a market benchmark.

Rather than focusing on short-term return prediction, this project emphasizes portfolio construction, downside risk measurement, factor exposure analysis, and out-of-sample robustness.

Four portfolio strategies are implemented and compared:

- Equal Weight Portfolio
- Minimum Variance Portfolio
- Maximum Sharpe Portfolio
- Risk Parity Portfolio

The strategies are evaluated using rolling-window backtesting, transaction cost analysis, stress testing, covariance shrinkage methods, parameter sensitivity analysis, and factor regression.

The project is implemented in Python using financial data processing, numerical optimization, statistical modeling, and visualization techniques.


---

# 2. Research Questions

The project investigates three main research questions:

### Question 1:
Can quantitative portfolio optimization methods improve risk-adjusted performance compared with a simple market benchmark?

### Question 2:
How do different portfolio construction methods behave under different market environments and risk conditions?

### Question 3:
Are portfolio performance results robust to practical considerations such as transaction costs, covariance estimation methods, and parameter choices?


---

# 3. Data and Asset Universe

The analysis uses exchange-traded funds (ETFs) representing different asset classes:

| Ticker | Asset Exposure |
|---|---|
| SPY | U.S. Large-Cap Equity Benchmark |
| QQQ | Technology and Growth Equity |
| IWM | U.S. Small-Cap Equity |
| TLT | Long-Term Treasury Bonds |
| GLD | Gold |
| VNQ | Real Estate Investment Trusts |
| EFA | International Developed Markets Equity |

Daily adjusted closing prices are collected and transformed into daily and monthly returns.

The sample period covers:

**January 2015 - December 2025**

SPY is used as the market benchmark for performance comparison.


---

# 4. Portfolio Construction Methodology

Four portfolio optimization methods are implemented.


## 4.1 Equal Weight Portfolio

The equal weight portfolio assigns identical weights to all assets:

\[
w_i=\frac{1}{N}
\]

This strategy provides a simple benchmark for comparison.


## 4.2 Minimum Variance Portfolio

The minimum variance portfolio solves:

\[
minimize \quad w^T\Sigma w
\]

where:

- \(w\) represents portfolio weights
- \(\Sigma\) represents the covariance matrix

The objective is to construct the lowest volatility portfolio under long-only constraints.


## 4.3 Maximum Sharpe Portfolio

The maximum Sharpe portfolio maximizes:

\[
Sharpe=\frac{R_p-R_f}{\sigma_p}
\]

where:

- \(R_p\) is portfolio return
- \(R_f\) is the risk-free rate
- \(\sigma_p\) is portfolio volatility

This strategy seeks the highest risk-adjusted return.


## 4.4 Risk Parity Portfolio

The risk parity strategy allocates weights according to risk contribution rather than capital allocation.

The objective is to equalize each asset's contribution to total portfolio risk.

This approach emphasizes diversification and portfolio stability.


---

# 5. Rolling Window Backtesting Framework

To avoid look-ahead bias, an out-of-sample rolling-window backtesting framework is implemented.

The baseline setting uses:

- Lookback window: 252 trading days
- Rebalancing frequency: 21 trading days


At each rebalance date:

1. Historical data from the previous estimation window is used to estimate portfolio parameters.
2. Portfolio weights are optimized.
3. The portfolio is evaluated on future unseen returns.


This framework provides a more realistic evaluation of portfolio performance compared with full-sample optimization.


---

# 6. Performance and Risk Evaluation

Portfolio performance is evaluated using both return-based and downside risk metrics.


The main evaluation metrics include:

- Annualized Return
- Annualized Volatility
- Sharpe Ratio
- Maximum Drawdown
- Historical Value-at-Risk (VaR)
- Historical Conditional Value-at-Risk (CVaR)
- Rolling Volatility


The analysis emphasizes risk-adjusted performance and downside protection rather than simply maximizing returns.


---

# 7. Transaction Costs and Turnover Analysis

To improve practical relevance, transaction costs and portfolio turnover are incorporated into the backtesting framework.

Portfolio turnover is calculated during each rebalance period:

\[
Turnover=\sum |w_t-w_{t-1}|
\]


Transaction costs are deducted from gross portfolio returns to obtain net performance.

The results show that transaction costs reduce realized portfolio performance, but the relative ranking of portfolio strategies remains broadly stable.

This analysis highlights the importance of considering implementation constraints when evaluating quantitative strategies.


---

# 8. Stress Testing

Portfolio strategies are evaluated during major market stress periods:

- COVID-19 market crash
- 2022 interest rate hiking period


Stress testing focuses on:

- Period return
- Volatility
- Maximum drawdown
- Historical VaR
- Historical CVaR


The results demonstrate that different portfolio construction methods exhibit different levels of downside protection during stressed market environments.

Risk-oriented strategies generally provide stronger defensive characteristics compared with equity-heavy portfolios.


---

# 9. Robustness Analysis


## 9.1 Ledoit-Wolf Covariance Shrinkage

Portfolio optimization is highly sensitive to covariance estimation errors.

To improve covariance estimation stability, Ledoit-Wolf shrinkage covariance estimation is implemented and compared with traditional sample covariance estimation.


The results show:

- Ledoit-Wolf slightly improves the minimum variance strategy.
- The Sharpe ratio increases due to more stable risk estimation.
- Maximum Sharpe optimization does not significantly improve, suggesting that expected return estimation remains a major source of uncertainty.


These findings highlight that robust covariance estimation can improve risk-based strategies but cannot completely eliminate estimation risk.


---

## 9.2 Parameter Sensitivity Analysis

To evaluate whether strategy performance depends on specific parameter choices, sensitivity analysis is conducted across different:

- Lookback windows:
  - 126 trading days
  - 252 trading days
  - 504 trading days

- Rebalancing frequencies:
  - 21 trading days
  - 63 trading days


The results indicate:

- Risk parity demonstrates relatively stable performance across different parameter settings.
- Maximum Sharpe optimization achieves strong performance under certain settings but shows higher sensitivity to parameter choices.
- Strategies relying heavily on expected return estimation are more vulnerable to estimation uncertainty.


This robustness analysis reduces concerns regarding overfitting and improves confidence in the evaluation results.


---

# 10. Factor Exposure Analysis

To understand the sources of portfolio returns, Fama-French factor regression is performed.

The regression model is:

\[
R_p-R_f=
\alpha+
\beta_1(MKT-RF)
+\beta_2SMB
+\beta_3HML
+\epsilon
\]


The analysis evaluates:

- Alpha
- Market exposure
- Size exposure
- Value exposure
- R-squared


Factor regression demonstrates that different portfolio strategies have distinct systematic risk exposures.

Rather than assuming excess returns are generated purely by optimization, the analysis examines whether performance can be explained by underlying market factors.


---

# 11. Key Findings

The main findings of this project are:


### 1. Portfolio optimization methods provide different risk-return characteristics.

No single optimization method dominates across all evaluation dimensions.


### 2. Risk parity provides relatively robust performance.

Among optimized portfolios, risk parity demonstrates stronger stability across different parameter settings and market conditions.


### 3. Maximum Sharpe optimization is sensitive to estimation assumptions.

Although maximum Sharpe optimization can achieve strong performance under certain conditions, its dependence on expected return estimates creates higher parameter sensitivity.


### 4. Transaction costs matter for practical implementation.

Ignoring turnover and trading costs may overestimate real-world portfolio performance.


### 5. Robust covariance estimation improves risk estimation.

Ledoit-Wolf shrinkage provides more stable covariance estimates and improves certain risk-based strategies.


### 6. Portfolio returns are partially explained by systematic risk factors.

Factor regression provides additional interpretation of strategy behavior beyond raw performance statistics.


---

# 12. Limitations and Future Improvements

Several limitations remain.


## Limitations

1. Historical returns may not accurately predict future performance.

2. Expected return estimation remains challenging in mean-variance optimization.

3. Transaction cost assumptions are simplified.

4. The current framework focuses on long-only portfolio constraints.

5. ETF-based analysis may not capture individual security-level opportunities.


## Future Improvements

Potential extensions include:

- Black-Litterman portfolio optimization
- Multi-factor equity selection models
- Dynamic asset allocation models
- Regime-switching approaches
- Machine learning-based return forecasting


---

# Conclusion

This project develops a quantitative portfolio optimization and risk management framework combining modern portfolio theory, statistical risk analysis, factor modeling, and robustness testing.

The results demonstrate that evaluating investment strategies requires not only return analysis but also careful consideration of downside risk, implementation costs, parameter sensitivity, and systematic risk exposure.

The project provides a practical application of quantitative methods to financial decision-making and demonstrates the connection between actuarial risk management, statistical modeling, and quantitative finance.
