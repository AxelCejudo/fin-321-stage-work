# Stage 5 – Final FX Hedge Recommendation  
**Analyst:** Axel Cejudo  
**Course:** FIN 321  
**Date:** December 2025  

---

## A. Exposure Summary

Our firm expects to receive **€5,000,000 in 90 days** from a European customer.  
Because our reporting currency is USD, this creates direct exposure to movements in **EUR/USD**. A euro depreciation would reduce our dollar-denominated revenue, affecting short-term liquidity, operating cash flow, and quarterly earnings stability. With the spot rate currently at **1.10 USD/EUR**, even a modest decline introduces material downside risk.

To manage this exposure, we evaluated three hedging strategies using our Stage 4 Excel model: a forward contract, a money market hedge, and a EUR put option. All calculations incorporate interest rate differentials, transaction costs, and hedge mechanics consistent with Stage 2 specifications.

---

## B. Summary of Hedge Outcomes

Using the model outputs:

### **Forward Hedge**
- **Locked-in USD proceeds:** **$5,594,400**
- Highest deterministic payout
- No exposure to future EUR/USD movements  
- Small transaction cost already incorporated

### **Money Market Hedge**
- **USD proceeds at maturity:** **$5,521,835.82**
- Slightly lower than the forward, but still stable
- Reflects synthetic forward created using borrowing/lending rates
- Payout remains flat across all spot rate scenarios

### **Put Option Hedge**
- **Net USD proceeds at Sₜ = 1.10:** **$5,400,000**
- Provides downside protection with upside potential  
- Most expensive strategy due to premium cost  
- Becomes attractive only if the euro appreciates meaningfully above 1.12

### **Unhedged Benchmark**
- **USD proceeds = €5M × Sₜ**
- Highly volatile  
- Ranges from **$5.225M** (Sₜ = 1.045 equivalent) to **$5.775M** (Sₜ = 1.155)

---

## C. Sensitivity Interpretation

### **EUR Depreciation (Downside Scenarios)**  
When the euro weakens (Sₜ < 1.10):
- **Unhedged proceeds drop sharply**, exposing revenue to FX volatility.
- **The forward and MM hedge remain flat**, eliminating downside variance.
- **The option underperforms** due to its premium but still protects the firm because the strike (1.08) sets a floor on EUR value.

### **EUR Appreciation (Upside Scenarios)**
When the euro strengthens:
- **Unhedged proceeds rise** proportionally.
- **The forward and MM hedge do not participate** in upside.
- **The option hedge captures upside** once Sₜ exceeds the strike, but only after recovering the premium cost.

In all reasonable ranges (±5%), the forward hedge delivers the **highest certain USD value** and the **best risk-adjusted outcome**.

---

## D. Strategic Recommendation

### **Recommended Strategy: Forward Hedge**

The **forward contract** provides the best balance of certainty, value, and simplicity:

1. **Highest guaranteed payout** ($5.594M) among all hedging methods.  
2. **Zero FX variance**, ensuring predictable USD cash flow.  
3. **Minimal operational complexity** compared to money market mechanics.  
4. **Lower economic cost** than purchasing optionality through a put.

Given that the firm’s priority is **cash flow stability and earnings predictability**, the forward hedge aligns most closely with management objectives. The money market hedge is acceptable but inferior in value. The option hedge is only justified if the firm has a strong, directional expectation of EUR appreciation — which we do not assume.

---

## E. Executive Justification

From a CFO perspective, the forward hedge offers:

- **Budget certainty:** Locks revenue for quarterly planning.
- **Liquidity clarity:** No ambiguity around dollar inflows in 90 days.
- **Cost efficiency:** Lower cost relative to option premia.
- **Operational simplicity:** One contract, no borrowing or reinvestment needed.
- **Accounting clarity:** Straightforward hedge documentation and effectiveness testing.

Meanwhile:

- The **MM hedge** is close in value but introduces unnecessary operational steps.  
- The **option hedge** provides flexibility but at a high premium cost that reduces expected value.

For these reasons, the firm should execute a **90-day EUR forward contract** to fully hedge the receivable.

---

# Extra Credit — Areas for Further Study & Improvement

## 1. AI Automation via Claude Skills  
A Claude Skill could automatically:
- Pull real-time EUR/USD spot and forward curves  
- Refresh interest rate inputs  
- Regenerate the full Stage 4 Excel model on demand  
- Instantly summarize updated hedge outcomes for treasury  

This removes manual data collection and ensures faster, more accurate daily exposure management.

## 2. OpenAI Code Interpreter / Codex  
Codex could:
- Translate all hedge logic into Python  
- Run Monte Carlo FX simulations  
- Validate Excel formulas against source logic  
- Programmatically generate updated hedge tables and charts  

This reduces human modeling error and provides a replicable audit trail.

## 3. Multi-File Reasoning for Model Governance  
LLMs can understand:
- The Stage 2 specification  
- The Stage 3 prototype Excel  
- The Stage 4 AI-generated workbook  

They can rebuild or cross-check the entire pipeline, ensuring consistency across versions and eliminating silent errors during spreadsheet edits.

## 4. GitHub Version Control (REQUIRED DISCUSSION)  
GitHub provides:
- A permanent history of all modeling stages  
- Commit-based traceability for audit and compliance  
- A clear separation between specification, prompt, and model outputs  
- Collaborative workflows (branches, pull requests) enabling peer review  

This mirrors real treasury environments where model governance and reproducibility are mandatory.

---

# Final Note

This project demonstrates the full modeling lifecycle used in modern corporate treasury:
specification → model → AI automation → executive decision-making.  
The forward hedge offers the strongest financial and strategic outcome for the firm.

