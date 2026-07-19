# Quantitative Portfolio Optimization and Risk Management with Factor Analysis

## 1. Project Overview

This project investigates whether portfolio optimization methods can improve risk-adjusted performance compared with a simple equity benchmark. The analysis focuses on portfolio construction, rolling-window backtesting, downside risk measurement, and Fama-French factor regression.

The project compares four portfolio strategies across major asset-class ETFs:

- Equal Weight
- Minimum Variance
- Maximum Sharpe
- Risk Parity

The SPY ETF is used as the benchmark.

## 2. Data

The project uses daily historical ETF price data from 2015 to 2025. The selected ETFs represent different asset classes and risk exposures:

| Ticker | Asset Class                       |
| ------ | --------------------------------- |
| SPY    | U.S. large-cap equity             |
| QQQ    | U.S. technology and growth equity |
| IWM    | U.S. small-cap equity             |
| TLT    | Long-term U.S. Treasury bonds     |
| GLD    | Gold                              |
| VNQ    | U.S. real estate                  |
| EFA    | Developed international equity    |

Daily returns and monthly returns are calculated from historical price data. The analysis focuses on price-based returns.

## 3. Methodology

The project first conducts static portfolio optimization using the full sample to understand the behavior of different allocation methods. It then performs a rolling-window backtest to evaluate out-of-sample performance.

The rolling-window backtest uses:

- 252 trading days as the estimation window
- 21 trading days as the rebalancing window
- Long-only portfolio weights
- Full investment constraint, where weights sum to one

The following performance and risk metrics are calculated:

- Annualized return
- Annualized volatility
- Sharpe ratio
- Maximum drawdown
- 95% historical VaR
- 95% historical CVaR

Finally, Fama-French three-factor regression is used to analyze each strategy's exposure to market, size, and value factors.

## 4. Static Optimization Results

The static optimization results show that different portfolio construction methods produce very different allocations. The minimum variance portfolio allocates more weight to defensive and diversifying assets such as TLT and GLD. The maximum Sharpe portfolio is more concentrated in GLD and QQQ, reflecting their strong historical risk-adjusted performance during the sample period.

However, static optimization uses the full sample and therefore should not be interpreted as true out-of-sample performance. The rolling-window backtest provides a more realistic evaluation.

## 5. Rolling Backtest Results

The rolling-window backtest shows that the SPY benchmark achieved the highest annualized return and the highest Sharpe ratio over the out-of-sample period. However, SPY also had the highest volatility and the largest downside risk.

| Strategy         | Annualized Return | Annualized Volatility | Sharpe Ratio |
| ---------------- | -----------------:| ---------------------:| ------------:|
| Equal Weight     | 9.70%             | 13.49%                | 0.571        |
| Minimum Variance | 7.11%             | 9.85%                 | 0.519        |
| Maximum Sharpe   | 9.12%             | 15.22%                | 0.468        |
| Risk Parity      | 9.37%             | 11.39%                | 0.647        |
| SPY Benchmark    | 14.05%            | 18.10%                | 0.665        |

Among the optimized strategies, the risk parity portfolio delivered the strongest risk-adjusted performance. Its Sharpe ratio was close to that of SPY, while its volatility was substantially lower.

## 6. Downside Risk Analysis

The downside risk results show that SPY had the largest drawdown and the most severe tail losses. This suggests that although SPY delivered the highest return, it also exposed investors to larger downside risk.

| Strategy         | Maximum Drawdown | 95% Historical VaR | 95% Historical CVaR |
| ---------------- | ----------------:| ------------------:| -------------------:|
| Equal Weight     | -27.58%          | -1.23%             | -1.99%              |
| Minimum Variance | -27.27%          | -0.94%             | -1.42%              |
| Maximum Sharpe   | -28.76%          | -1.52%             | -2.31%              |
| Risk Parity      | -26.97%          | -1.06%             | -1.70%              |
| SPY Benchmark    | -34.10%          | -1.69%             | -2.78%              |

The minimum variance portfolio achieved the lowest volatility and the smallest tail risk. The risk parity portfolio provided a strong balance between return and downside protection.

## 7. Factor Regression Results

The Fama-French three-factor regression shows that SPY is almost entirely explained by market exposure, with a market beta close to one and an R-squared above 0.99.

| Strategy         | Alpha     | Market Beta | SMB Beta | HML Beta | R-squared |
| ---------------- | ---------:| -----------:| --------:| --------:| ---------:|
| Equal Weight     | -0.000049 | 0.651       | 0.138    | -0.014   | 0.872     |
| Minimum Variance | 0.000034  | 0.292       | 0.025    | -0.110   | 0.356     |
| Maximum Sharpe   | 0.000012  | 0.475       | 0.051    | -0.227   | 0.419     |
| Risk Parity      | 0.000037  | 0.467       | 0.136    | -0.046   | 0.660     |
| SPY Benchmark    | -0.000072 | 0.982       | -0.121   | 0.019    | 0.992     |

The optimized portfolios have lower market betas than SPY, reflecting their diversification across bonds, gold, real estate, and international equities. The maximum Sharpe portfolio has a negative HML loading, consistent with its allocation toward growth-oriented assets such as QQQ.

The alpha estimates are close to zero, so the results should be interpreted as differences in factor exposure rather than evidence of persistent abnormal returns.

## 8. Limitations

This project has several limitations. First, the analysis does not fully model transaction costs, bid-ask spreads, taxes, or market liquidity constraints. Second, the optimization methods are sensitive to historical mean return and covariance estimates. Third, the analysis uses historical price-based returns, and historical performance does not guarantee future results.

## 9. Future Improvements

Future extensions could include:

- Transaction cost and turnover analysis
- Ledoit-Wolf covariance shrinkage
- Black-Litterman portfolio optimization
- Fama-French five-factor regression
- Stress testing during crisis periods
- Comparison with additional benchmarks

## 10. Conclusion

This project shows that portfolio optimization methods do not necessarily outperform a strong equity benchmark in terms of raw return. However, strategies such as risk parity and minimum variance can improve risk control by reducing volatility, drawdowns, and tail losses.

From a risk management perspective, the results highlight the importance of evaluating portfolios not only by return, but also by downside risk, factor exposure, and out-of-sample robustness.
