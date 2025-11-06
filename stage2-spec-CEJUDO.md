# Stage 2 Technical Specification – FX Hedge Model
**Analyst:** Axel Cejudo  
**Course:** FIN 321  
**Date:** November 7, 2025  
**File:** stage2-spec-CEJUDO.md

## 1. Problem Statement
The firm is scheduled to receive **€5,000,000** from a European customer in **90 days** as payment for exported goods. Our reporting currency is USD, exposing future cash flows to EUR/USD exchange rate volatility. Recent monetary policy divergence between the Federal Reserve and European Central Bank suggests elevated currency risk. If the euro depreciates prior to settlement, USD proceeds could materially decline, impacting revenue recognition and short-term liquidity. Our objective is to quantitatively compare alternative hedging strategies to lock in—or selectively protect—USD conversion value, and support a treasury recommendation prior to settlement :contentReference[oaicite:0]{index=0}.


## 2. Inputs (Known Variables)
All variables below must be explicitly parameterized within the model:

| Variable | Description | Units | Source |
|---------|-------------|-------|--------|
| EUR Receivable Amount | Contract value to be received | EUR | Client invoice |
| Settlement Horizon | Time until payment | Days | Contract terms |
| Spot FX Rate (S₀) | Current EUR/USD rate | USD/EUR | Market data feed |
| Forward FX Rate (F) | 90-day forward EUR/USD | USD/EUR | Market forward curve |
| EUR Interest Rate (r_EUR) | 90-day annualized funding rate | % annual | EUR money market |
| USD Interest Rate (r_USD) | 90-day annualized lending rate | % annual | U.S. money market |
| Option Premium | Cost to purchase EUR put (USD) | % of notional | Dealer quotes |
| Strike Price (K) | Option exercise FX rate | USD/EUR | Dealer quotes |
| Transaction Costs | Bid/ask spreads, fees | USD | Broker disclosures |
| Volatility Estimate | Annual implied volatility | % | Option quotes |

Key model drivers will be input in a dedicated assumptions tab to simplify versioning and scenario runs.


## 3. Assumptions & Constraints
- **Day Count Convention:** 30/360, simple interest basis for money market hedge.
- **Credit Quality:** Counterparty risk ignored; assume fully collateralized relationships.
- **Transaction Costs:** Modeled as a per-unit spread deduction rather than proportional slippage.
- **Liquidity:** Markets assumed sufficiently liquid at quoted rates.
- **Option Type:** European-style, cash-settled; no early exercise (simplifies payoff logic).
- **Premium Timing:** Premium paid at inception in USD.
- **Taxes:** Excluded.
- **Operational Constraints:** Treasury can borrow/lend at quoted deposit rates (no haircuts).
- **Regulatory Considerations:** Not modeled.

These constraints keep the mathematical flow transparent and realistically implementable.


## 4. Calculation Flow
The spreadsheet will implement three hedging path flows plus an unhedged baseline:

### (A) Unhedged Exposure
1. Select a future spot rate scenario (S_T).
2. Convert €5,000,000 at S_T.
3. Compute USD proceeds.
4. Compare across scenario grid.

Purpose: benchmark risk and variance.


### (B) Forward Hedge
1. Retrieve forward rate F(90-day).
2. Lock exchange rate today.
3. At maturity, convert full notional: €5,000,000 × F.
4. Output USD receipts (constant across spot outcomes).
5. Adjust for transaction spread if required.

Eliminates FX uncertainty entirely.


### (C) Money Market Hedge
1. Present-value discount the EUR receivable at r_EUR.
2. Borrow that EUR PV today.
3. Convert borrowed EUR to USD at spot.
4. Invest USD proceeds at r_USD for 90 days.
5. At maturity, repay EUR loan using received receivable.
6. Output matured USD investment value.

Creates synthetic forward via interest rate parity.


### (D) Options Hedge (EUR Put)
1. Select strike price K based on market quotes.
2. Pay premium upfront in USD.
3. At maturity:
   - If S_T < K, exercise → €5,000,000 × K.
   - If S_T ≥ K, allow to expire → convert at S_T.
4. USD Proceeds = Max(K, S_T) × €5,000,000 − Premium.
5. Present option payoff graphically.

Provides downside protection with upside flexibility.


## 5. Outputs
The model will generate:

### Core Metrics
- USD proceeds under:
  - Unhedged
  - Forward
  - Money market
  - Option
- Net benefit vs. unhedged baseline
- Hedge cost vs. locked-in stability
- Break-even FX levels

### Tables
- Scenario comparison matrix (multiple S_T values)
- Hedge payoff summary
- Premium sensitivity

### Charts
- Payoff diagrams (forward flat, option kinked)
- Scenario returns vs. FX rate chart
- Distribution of outcomes

Presentations should visually emphasize risk reduction vs. potential upside sacrifice.


## 6. Sensitivity Plan
The spreadsheet will simulate outcomes across:

### Spot FX Scenarios
- −10%, −5%, 0%, +5%, +10% from current spot
- Custom user-defined values

### Interest Rate Shocks
- +/− 50 bps to EUR and USD rates

### Volatility Impact (Options Only)
- Premium recalculated using implied volatility multipliers:
  - −20%, baseline, +20%

Visualization:
- Tornado chart (key drivers)
- Fan chart (future FX dispersion)
- Comparative payoff lines

Sensitivity tools allow treasury to stress-test adverse macro paths.


## 7. Limitations & Next Steps
### Limitations
- Model does not incorporate:
  - Counterparty credit adjustments
  - Intraday liquidity stress
  - Dealer collateral margining
  - Basis swaps or more exotic hedges
- Taxes and accounting treatment (ASC 815) not modeled.
- Option pricing treated using market premium input, not Black-Scholes calculation.

### Next Steps (Stage 3 Excel Build)
- Implement spreadsheet tabs:
  - Inputs & Assumptions
  - Hedge Engines (Forward, MM, Option)
  - Sensitivity Tables
  - Scenario Dashboard
- Build automated comparison output.
- Design AI prompt to regenerate the model from parameter sheet.

This specification enables reproducible hedge evaluation and data-driven CFO decision-making.

