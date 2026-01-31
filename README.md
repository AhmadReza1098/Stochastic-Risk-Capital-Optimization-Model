# Stochastic Risk Capital Optimization Model (Indian Insurance Sector)

![Excel](https://img.shields.io/badge/Tool-Microsoft%20Excel-green) ![Technique](https://img.shields.io/badge/Method-Monte%20Carlo%20Simulation-blue) ![Optimization](https://img.shields.io/badge/Solver-Non--Linear%20GRG-orange) ![Status](https://img.shields.io/badge/Status-Basel%20III%20Compliant-success)

## 📌 Executive Summary
This project is a **Stochastic Capital Adequacy Model** designed for the Indian General Insurance sector. It simulates **1,000 correlated market scenarios** to calculate the optimal capital buffer required to withstand catastrophic (1-in-100-year) events.

Unlike standard static models, this engine uses **Cholesky Decomposition** to preserve the correlation between assets during market crashes, ensuring that "Tail Risks" are accurately captured.

**Key Outcome:** The model optimized the portfolio allocation (shifting 75% capital to ICICI Lombard), reducing annualized volatility from **32.7% to 26.4%** while maintaining a robust **Solvency Coverage Ratio of ~2.88x**.

---

## 📊 The Business Problem
Indian insurers (ICICI Lombard, GIC Re, NIACL) face unique risks where regulatory capital often underestimates the impact of simultaneous market crashes ("Fat Tail" events).
* **The Challenge:** How much liquid capital must be held in reserve to survive a "High CAT (Catastrophe)" event without becoming insolvent?
* **The Solution:** A dynamic Monte Carlo simulation that stress-tests the portfolio against regulatory shifts and disaster scenarios.

---

## ⚙️ Technical Methodology

### 1. Data & Correlation (Cholesky Decomposition)
* **Data Source:** Historical daily returns (2020–2025) for ICICI Lombard, GIC Re, and New India Assurance (NIACL).
* **Mathematics:** Implemented **Cholesky Decomposition** to transform independent random variables into correlated variables. This ensures that if GIC Re crashes, the simulation correctly predicts the drag on NIACL.

### 2. Stochastic Simulation (Monte Carlo)
* Ran **1,000 iterations** using a Gaussian Copula approach.
* Calculated **VaR (Value at Risk)** and **TVaR (Tail Value at Risk)** at the 99% confidence level to quantify the "Expected Shortfall."

### 3. Non-Linear Optimization (Excel Solver)
* **Objective:** Minimize Portfolio Variance subject to a target return.
* **Constraints:** Fully invested (Sum of weights = 100%), No short selling.
* **Result:** Identified an optimal mix of **75% ICICI / 20% GIC / 5% NIACL**, creating a "Diversification Benefit" of ~1.8%.

### 4. Model Validation (Backtesting)
* Performed a **Basel Traffic Light Backtest** over a 1,250-day historical window.
* **Result:** The model produced only **6 exceptions**, placing it in the **"Green Zone"** (statistically valid) under Basel III capital requirements.

---

## 📈 Dashboard & Scenario Analysis

The project features a dynamic **Executive Dashboard** allowing users to toggle between stress scenarios:

| Scenario | Definition | TVaR (Tail Loss) | Verdict |
| :--- | :--- | :--- | :--- |
| **Regulatory Shift** | Hypothetical efficiency gains in NIACL | **-2.65%** | ✅ Opportunity |
| **Base Case** | Standard market operating conditions | **-2.95%** | ✅ Baseline |
| **High CAT Loss** | 1-in-100-year disaster (-0.50% daily shock to GIC) | **-5.40%** | ⚠️ Critical Stress |

*(Note: The Solvency Ratio remains >1.5x even in the High CAT scenario, proving portfolio resilience.)*

---

## 📂 Project Structure

```text
├── Executive_Dashboard     # The "Control Tower" (Scenario Selector, Solvency Box, Risk Histogram)
├── Scenario_Analysis       # The "What-If" Engine driving the dynamic parameters
├── Monte_Carlo             # The Core Engine (1,000 Rows of Cholesky Simulation)
├── Backtest_&_ES           # Regulatory Validation (Basel Traffic Light Logic)
├── Historical_Sim          # Historical VaR calculation for comparison
└── Raw_Data                # Cleaned price data (2020-2025)
