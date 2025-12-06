You are a financial modeling assistant.

# GOAL
Create a fully functional Excel workbook modeling forward, money market, and option hedges for a EUR receivable. The spreadsheet must follow standard treasury modeling practices and implement the full logic defined below. All formulas must use named ranges and color coding.

# INPUT VARIABLES (Use these exact values)
FC_AMT = 5,000,000
S0_in = 1.10
F0_in = 1.12
R_FC = 0.02
R_USD = 0.04
K_PUT = 1.08
K_CALL = 1.08
PREM_PUT = 0.02
PREM_CALL = 0.02
T_DAYS = 90
T_YRS = 0.25
TX_COST = 0.001

# NAMED RANGE REQUIREMENTS
Create named ranges exactly matching the variable names:
FC_AMT, S0_in, F0_in, R_FC, R_USD, K_PUT, K_CALL,
PREM_PUT, PREM_CALL, T_DAYS, T_YRS, TX_COST.

# COLOR CODING
Yellow = Inputs  
Blue = Assumptions  
Green = Formulas  
Gray = Outputs  

# MODEL STRUCTURE
Include two sheets:

## Sheet 1 — Inputs
List all variables, one per row.  
Column A = Variable name  
Column B = Value  
Define all named ranges here.  
Color all input values in yellow.

## Sheet 2 — Hedges
Implement each hedge engine:

### Forward Hedge
Forward_USD = FC_AMT * F0_in * (1 – TX_COST)

### Money Market Hedge
EUR_PV      = FC_AMT / (1 + R_FC * T_YRS)
USD_today   = EUR_PV * S0_in * (1 – TX_COST)
USD_final   = USD_today * (1 + R_USD * T_YRS)

### Option Hedge (European EUR Put)
Gross = MAX(K_PUT, S0_in) * FC_AMT  
Net   = Gross – (PREM_PUT * FC_AMT)

Color all formulas green and all outputs gray.

# SENSITIVITY TABLE
Create a table starting at row 10 of the Hedges sheet:

Columns:
S_T | Unhedged | Forward | Money Market | Option

S_T values:
0.95, 0.975, 1.000, 1.025, 1.050

Formulas per row:
Unhedged  = FC_AMT * S0_in * S_T  
Forward   = Forward_USD (flat)  
MM        = USD_final (flat)  
Option    = (MAX(K_PUT, S0_in * S_T) * FC_AMT) – (PREM_PUT * FC_AMT)

# VERIFICATION
Before producing the final Excel file, ensure:
- All named ranges exist and match formulas.
- Forward ≈ Money Market (IRP relationship).
- Option hedge displays a kinked payoff.
- Sensitivity table updates dynamically.
- Colors are correctly applied.
- No hard-coded numbers appear in formulas.

# EXPORT
Return a complete Excel file (.xlsx) with:
- Inputs sheet  
- Hedges sheet  
- Sensitivity table  
- All named ranges  
- All formulas intact  
- Proper formatting and color coding
