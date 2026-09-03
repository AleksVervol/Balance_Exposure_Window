# Stablecoin Settlement Resilience

### Stress Testing Operational Crypto Balances Across Market, Liquidity, and Banking Shocks

## Project Overview

This project examines whether converting volatile crypto assets into **stablecoins such as USDT or USDC** effectively protects operational payment balances during periods of market stress.

In a crypto payment operation, incoming volatile assets may be converted into stablecoins to reduce direct exposure to BTC and ETH price volatility. However, stablecoin-denominated balances are not risk-free. Their resilience may depend on the stability of the peg, the issuer's reserve infrastructure, the counterparty holding the funds, and whether the balance remains operationally accessible.

The project therefore separates two analytical layers:

- **Market stress layer — BTC & ETH:** used to measure the severity and timing of broader crypto-market movements.
- **Operational balance layer — USDT & USDC:** used to evaluate valuation stability and operational usability of the assets in which payment balances may actually be held.

The goal is not to prove that stablecoins are safe or unsafe. The goal is to identify **which risks stablecoin conversion reduces, which risks remain, and which risks cannot be detected from price data alone**.

---

## Business Question

> **When does holding operational balances in stablecoins effectively protect a crypto payment operation from market volatility, and under what conditions does the stablecoin or its infrastructure become a source of risk?**

---

## Stress Scenarios

| Event | Risk mechanism | Main question | Current status |
|---|---|---|---|
| **LUNA / UST collapse — May 2022** | Stablecoin failure / contagion | Did the collapse of UST create measurable peg stress in USDT or USDC? | ✅ EDA completed |
| **Celsius withdrawal halt — June 2022** | Counterparty / access risk | Can a stablecoin balance retain market value while becoming operationally unavailable? | ✅ EDA completed |
| **SVB collapse / USDC depeg — March 2023** | Reserve / banking infrastructure risk | What happens when a shock directly affects reserves supporting a stablecoin? | 🔄 In progress |
| **2024 US election market rally — November 2024** | Positive market-wide shock | Do USDT and USDC remain stable during strong bullish market movements? | ⏳ Pending |

---

## Research Hypotheses

### H1 — Market-volatility protection

USDT and USDC will show substantially smaller price deviations than BTC and ETH during broad cryptocurrency market shocks.

If supported, this would indicate that conversion into stablecoins can reduce direct exposure to BTC/ETH volatility.

### H2 — Stablecoin contagion

The failure of another major stablecoin may create temporary peg stress in USDT and/or USDC even without direct issuer exposure.

The LUNA / UST collapse is used as the main test case.

### H3 — Direct reserve exposure

A shock directly affecting a stablecoin issuer's reserves can produce materially greater peg instability than general cryptocurrency market volatility.

The SVB / USDC event is used as the main test case.

### H4 — Positive-market resilience

Strong positive crypto-market movements do not necessarily destabilize stablecoin pegs to the same extent as redemption, liquidity, or reserve-related stress.

The November 2024 market rally is used as a comparison case.

### Access-risk proposition

Price stability alone is not sufficient to determine whether an operational balance is safe.

The Celsius case tests the proposition that:

> **Market value and operational availability are different dimensions of risk.**

---

## Analytical Framework

```text
MARKET CONTEXT
BTC / ETH
    ↓
How severe was the broader market move?

EVENT DEFINITION
Historical event timeline
    ↓
Define a defensible T0 reference point

OPERATIONAL BALANCE
USDT / USDC
    ↓
How did the balance behave during the same stress event?

RISK MECHANISM
    ↓
LUNA    → peg / contagion risk
Celsius → counterparty / access risk
SVB     → reserve / banking infrastructure risk
Trump   → positive-market comparison
```

The exact quantitative analysis differs by event because each scenario represents a different risk mechanism.

---

## Core Metrics

For stablecoin valuation-risk cases, the project uses:

- **Peg deviation** — distance from the intended $1 reference value.
- **Maximum negative peg deviation** — worst observed deviation within the event window.
- **Threshold persistence** — number of hourly observations below selected levels such as `$0.995`, `$0.990`, and `$0.980`.
- **Recovery time** — time required to return above a defined tolerance threshold after the lowest point.
- **Operational balance impact** — translation of market movements into the value of a hypothetical operational balance.

For counterparty/access-risk scenarios, additional measures are used:

- **Market Value** — observed EUR value of the stablecoin balance.
- **Available Operational Liquidity** — value that can actually be accessed for payments or settlements.
- **Availability Ratio** — share of market value that remains operationally accessible.
- **Liquidity at Risk** — market value that exists but is unavailable for operational use.

---

## Findings So Far

### LUNA / UST

The LUNA event showed that stablecoins can behave differently under the same broader market shock.

In the current analysis:

- USDT reached a minimum implied USD value of approximately **$0.9716 (-2.84%)**.
- USDT recorded **13 consecutive hourly observations below $0.995**.
- USDT recovered above the $0.995 threshold **10 hours after its lowest point**.
- USDC remained within the selected 0.5% tolerance threshold during the event window.

This suggests that stablecoin conversion can reduce direct BTC/ETH exposure, while still leaving residual peg and contagion risk.

### Celsius

The Celsius case focuses on **access risk rather than peg failure**.

A deterministic stress scenario models a hypothetical **100,000 USDT operational balance**:

- immediately after the withdrawal halt, the balance retained a market value of approximately **€95.2k**;
- under the Celsius scenario, modeled operational availability fell to **0%**;
- approximately **€95.2k of market-valued liquidity became unavailable for operational use**;
- the same balance on an unaffected accessible venue remained fully usable.

The key finding is:

> **A balance can retain market value while losing operational liquidity.**

---

## Key Terms

**Stablecoin**  
A crypto asset designed to maintain a stable value relative to another asset. USDT and USDC are designed to track the US dollar.

**Peg**  
The target value a stablecoin is designed to maintain. For USDT and USDC, the target is approximately $1.

**Depeg**  
A movement away from the intended stablecoin peg.

**Operational Balance**  
Funds held to support day-to-day payment activities such as payouts, settlements, and liquidity management.

**Settlement**  
Completion of a payment or transfer when funds are delivered and become available to the receiving party.

**Operational Liquidity**  
The portion of an operational balance that is accessible and available for operational use.

**Market Value**  
The current value of an asset based on its observed market price.

**Liquidity at Risk**  
In this project, market value that exists but is unavailable for operational use.

**Counterparty Risk**  
The risk that an external party holding or facilitating funds cannot meet its obligations or provide access to those funds.

**Access Risk**  
The risk that funds retain economic value but cannot be accessed or transferred when needed.

**Market Stress**  
A period of unusually large or rapid market movements.

**Event Window**  
The period before and after a selected historical event used for analysis.

**T0 (Event Time)**  
The reference timestamp assigned to a specific event for before-and-after analysis.

---

## Data Sources

The project currently combines several public market-data sources:

- **yfinance** — daily BTC, ETH, USDT and USDC market data used for broader historical context.
- **Binance public API** — hourly BTC/USDT and ETH/USDT market data.
- **Coinbase Exchange API** — hourly USDT/EUR and USDC/EUR market data.
- **Dukascopy** — hourly EUR/USD FX data used where USD-equivalent stablecoin values are required.
- **Public event sources** — used to establish defensible event timelines and T0 reference points.

Raw and processed datasets are excluded from the repository and can be recreated through the project data-ingestion pipeline.

---

## Project Structure

```text
stablecoin-settlement-resilience/
│
├── data/                       # excluded from Git
│
├── notebooks/
│   ├── 01_data_ingestion.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03a_data_exploration_luna.ipynb
│   ├── 03b_data_exploration_celsius.ipynb
│   └── ...
│
├── .gitignore
└── README.md
```

The project will later include the SQL/dbt transformation layer and final Tableau outputs.

---

## Current Progress

- [x] Project scope and hypotheses revised
- [x] Data ingestion pipeline
- [x] Data cleaning and validation
- [x] LUNA event EDA
- [x] Celsius event EDA
- [ ] SVB / USDC event EDA
- [ ] November 2024 positive-market event EDA
- [ ] Cross-event comparison
- [ ] DuckDB + SQL/dbt transformation layer
- [ ] Final Tableau dashboard
- [ ] Final conclusions and recommendations

---

## Technology

- **Python / Jupyter** — data ingestion, cleaning, validation, EDA, scenario modelling
- **DuckDB** — local analytical database
- **SQL + dbt Core** — planned transformation and reusable risk-metric models
- **Tableau** — planned final event comparison and risk visualization

---

## Project Status

**Work in progress.**

The repository is updated incrementally so that the development of the analytical framework, assumptions, event research, and findings can be tracked throughout the project.
