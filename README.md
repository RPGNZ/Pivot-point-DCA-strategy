# 📊 Pivot Point–Based DCA Strategy vs. Regular DCA

## Overview

Background idea is that stocks are often attracted to pivot points. Assuming, the price could eventually go down to pivot levels, they could be more interesting entry points than just DCA periodic open prices.

Bellow chart shows an example where market price hits several times weekly pivot levels.

<img width="939" height="361" alt="NASDAQ_nov25_fev26" src="images/NASDAQ_nov25_fev26.png" />

This project implements and compares two systematic investment strategies:

1. **Regular Weekly DCA (Dollar-Cost Averaging)**
2. **Pivot Point–Based Weekly DCA**

The objective is to evaluate whether allocating weekly capital using technical pivot levels can improve capital efficiency compared to a standard weekly DCA approach.

The backtest includes:

- Full trade simulation  
- Cash tracking  
- Position sizing  
- Portfolio valuation  
- IRR computation (annualized)  
- Interactive visualization with Plotly  

## Strategy Description

### 1️⃣ Regular Weekly DCA

- Invests a fixed amount every week.
- Buys at the **open price of the first trading day of each new week**.
- Option to allow or disallow fractional shares.
- Uninvested cash is carried forward.

This strategy serves as the benchmark.

### 2️⃣ Pivot-Based Weekly DCA

Each week:

1. Weekly pivot levels are computed from the previous week's OHLC data:
   - P (Pivot)
   - R1, R2, R3 (Resistance levels)
   - S1, S2, S3 (Support levels)

2. Strategy logic:
   - If previous close is above EMA → buy at weekly open (behaves like regular DCA).
   - Otherwise:
     - Place limit orders at pivot levels below previous close.
     - Use up to `max_pivots` closest eligible levels.
     - Execute orders if price trades through pivot during the week.

3. Cash not deployed remains available for future weeks.

## Parameters

Available backtest parameters:

```python
ticker = "QQQ" # Ticker name
start_date = "2025-11-04" # Backtest start date
weekly_budget = 1000  # weekly budget to be invested
allow_fractional_shares = False # buy fractional shares of the asset
```

Pivot-point based DCA parameters:

```python
pivot_DCA_param = {
    "max_pivots": 2, # Depth of pivot levels to use
    "ema_filter": True, # Use price to EMA relative position to arbitrate whether to use pivot levels or buy at next week open price
    "ema_period": 14, # EMA period
    "pivot_colors": { # for display
        "S3": "red",
        "S2": "red",
        "S1": "orange",
        "P": "white",
        "R1": "cyan",
        "R2": "lime",
        "R3": "lime",
        }
}
```

## Performance Metrics

The following metrics are computed for both strategies:

- Total cash invested
- Final portfolio value
- Total return (non-annualized)
- Weekly IRR
- Annualized IRR (compounded weekly)

## Limitations

- No transaction costs
- No slippage modeling
- No tax considerations
- No liquidity constraints
- Assumes perfect order execution at pivot levels

## Disclaimer

This code is provided for educational and informational purposes only.
It does not constitute investment advice.
The author assumes no responsibility for financial decisions made based on this project.
