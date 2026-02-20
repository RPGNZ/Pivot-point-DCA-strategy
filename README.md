# 📊 Pivot Point–Based DCA Strategy vs. Regular DCA

## Overview

This project implements and compares two systematic investment strategies:

1. **Regular Weekly DCA (Dollar-Cost Averaging)**
2. **Pivot Point–Based Weekly DCA**

The objective is to evaluate whether allocating weekly capital using technical pivot levels (combined with an EMA filter) can improve capital efficiency compared to a standard weekly DCA approach.

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

---

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

---

## Performance Metrics

The following metrics are computed for both strategies:

- Total cash invested
- Final portfolio value
- Total return (non-annualized)
- Weekly IRR
- Annualized IRR (compounded weekly)

---

## Limitations

- No transaction costs
- No slippage modeling
- No tax considerations
- No liquidity constraints
- Assumes perfect order execution at pivot levels

This is a research / educational backtesting framework, not a production trading engine.

---

## Disclaimer

This code is provided for educational and informational purposes only.
It does not constitute investment advice.
The author assumes no responsibility for financial decisions made based on this project.
