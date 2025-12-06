Stage 4 – AI Prompt for Automated FX Hedge Model

Analyst: Axel Cejudo
Course: FIN 321
Deliverable: Stage 4 Structured AI Prompt (for full spreadsheet generation)

GOAL

You are a financial modeling assistant.
Create a fully functional Excel workbook that models forward, money market, and option hedges for my EUR receivable. The spreadsheet must exactly follow the logic defined in my Stage 2 Technical Specification and replicate the structure used in my Stage 3 Excel model. The goal is to generate a complete, professional, auditable hedge model automatically.

CONTEXT

This prompt must produce an Excel workbook that would allow a Treasury Analyst to evaluate EUR/USD FX exposure using:

Forward hedge

Money Market hedge

EUR put option hedge

Unhedged benchmark

A sensitivity table around future spot rates

The spreadsheet must be cleanly labeled, color-coded, and include named ranges for all assumptions and variables.

INPUT VARIABLES (Use exactly these values)

All of the following must appear as named ranges in the Excel model:

FC_AMT = 5,000,000
S0_in = 1.10
F0_in = 1.12
R_EUR = 0.02
R_USD = 0.04
K_PUT = 1.08
K_CALL = 0
PREM_PUT = 0.02 × FC_AMT × S0_in
PREM_CALL = 0
T_DAYS = 90
T_YRS = 0.25
TCOST = 0.001

Units:
Spot, forward, strike = USD/EUR
Interest rates = Annual simple
Premiums = USD
Notional = EUR

SPREADSHEET REQUIREMENTS

The spreadsheet must follow these structural and formatting rules:

Named Ranges
Create named ranges exactly as listed:
FC_AMT, S0_in, F0_in, R_USD, R_FC, K_PUT, K_CALL, PREM_PUT, PREM_CALL, T_DAYS, T_YRS, TCOST.

Color Coding
Yellow = Inputs (named ranges)
Blue = Assumptions
Green = Formulas
Gray = Outputs/KPIs

Model Components Required
The Excel file must include the following sections, each clearly labeled:

A. Unhedged USD Proceeds
USD = FC_AMT × S_T

B. Forward Hedge
USD = FC_AMT × F0_in × (1 − TCOST)

C. Money Market Hedge
EUR_PV = FC_AMT / (1 + R_EUR × T_YRS)
USD_today = EUR_PV × S0_in × (1 − TCOST)
USD_final = USD_today × (1 + R_USD × T_YRS)

D. Option Hedge (EUR Put)
Option premium = PREM_PUT
Payoff = MAX(K_PUT − S_T, 0) × FC_AMT
Net USD = Payoff − premium

E. Sensitivity Table
Create a table with S_T values from 0.95 × S0_in through 1.05 × S0_in with several increments.
For each S_T, calculate:
Unhedged
Forward
Money Market
Option

F. Summary Output Section
Show:
Unhedged USD
Forward Hedge USD
Money Market USD
Option USD
Highlight in gray which strategy delivers highest USD at base S_T = S0_in.

MODEL LOGIC (Explicit Instructions)

The AI must embed the following formulas into the sheet (using named ranges):

Forward Hedge
FC_AMT * F0_in * (1 - TCOST)

Money Market Hedge
EUR_PV = FC_AMT / (1 + R_EUR * T_YRS)
USD_TODAY = EUR_PV * S0_in * (1 - TCOST)
USD_FINAL = USD_TODAY * (1 + R_USD * T_YRS)

Option Hedge
Payoff = MAX(K_PUT - S_T, 0) * FC_AMT
Net = Payoff - PREM_PUT

Unhedged
USD = FC_AMT * S_T

Spot scenarios must automatically update all strategies.

FORMATTING REQUIREMENTS

The Excel workbook must be structured in a professional treasury-model layout:

Inputs and assumptions at the top
Hedge engines in the middle (Forward → MM → Option)
Sensitivity table at bottom
Summary at the end

Use thick borders to separate sections.
Use thousands separators.
Label all numbers with units (USD, EUR, USD/EUR).
All formulas must be visible and never hardcoded.

VERIFICATION REQUIREMENTS

Before producing the final file, the AI must verify:

All named ranges exist and are used in formulas.

Forward hedge ≈ Money Market hedge (interest rate parity check).

Option payoff decreases above strike and floors below strike.

Sensitivity table updates dynamically when S_T changes.

All color-coding rules are followed.

No calculations rely on hidden assumptions.

EXPORT INSTRUCTIONS

When complete, the model must be delivered as a fully functional downloadable Excel (.xlsx) file with all formulas preserved, correct formatting, and all named ranges applied.

END OF PROMPT
