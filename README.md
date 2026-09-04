# Stablecoin Settlement Resilience

### Stress Testing Operational Crypto Balances Across Market, Liquidity, and Banking Shocks

## Project Overview

This project models a crypto payment operation in which **incoming payments received in volatile cryptocurrencies are converted into USDT to reduce direct exposure to short-term BTC and ETH price movements**.

The project then stress-tests this modelled operational balance across several historical events to understand what risks the conversion may reduce — and what risks may still remain afterward.

The analysis separates three roles:

- **BTC and ETH — broader market context**  
  These assets represent the volatile side of the model and are used to measure the timing and magnitude of broader crypto-market movements.

- **USDT — modelled operational balance**  
  Incoming volatile crypto payments are assumed to be converted into USDT.

- **USDC — comparison stablecoin**  
  USDC is used to help distinguish broader stablecoin-market stress from movements that may be specific to one asset.

The project does not treat stablecoin conversion as risk-free. Even after direct BTC and ETH exposure is reduced, the operational balance may still be affected by peg instability, counterparty restrictions, reserve infrastructure, and asset accessibility.

The goal is to identify **which risks the modelled conversion strategy reduces, which risks remain, and which risks cannot be detected from market-price data alone**.

---

## Business Question

> **What risks are reduced when incoming volatile crypto payments are converted into USDT for operational use, and what risks remain under different market, liquidity, and infrastructure stress scenarios?**

---

## Stress Scenarios

| Event | Risk mechanism | Main question | Status |
|---|---|---|---|
| **LUNA / UST collapse — May 2022** | Stablecoin contagion / peg risk | Can the failure of another stablecoin affect the value of the modelled USDT operational balance? | ✅ EDA completed |
| **Celsius withdrawal halt — June 2022** | Counterparty / access risk | Can a USDT balance retain market value while becoming operationally unavailable? | ✅ EDA completed |
| **SVB / USDC depeg — March 2023** | Reserve / banking infrastructure risk | Can problems with the reserves supporting one stablecoin create severe instability while USDT remains comparatively stable? | ✅ EDA completed |
| **2024 U.S. election rally — November 2024** | Positive-market comparison | Does the USDT operational balance remain stable while BTC and ETH rise strongly? | ✅ EDA completed |

---

## Research Hypotheses

### H1 — Market-volatility protection

The modelled USDT operational balance will show substantially smaller price movements than BTC and ETH during broad crypto-market stress.

If supported, this would indicate that conversion into USDT reduces direct exposure to volatile crypto-market movements.

### H2 — Stablecoin contagion

The failure of another major stablecoin may create temporary peg stress in USDT even without direct issuer exposure.

The LUNA / UST collapse is used as the main test case.

### H3 — Stablecoin-specific reserve risk

A shock affecting the reserve infrastructure of a stablecoin can create materially greater instability in that stablecoin than in USDT under the same broader market conditions.

The SVB / USDC event is used as the main test case.

### H4 — Positive-market resilience

Strong positive BTC and ETH movements will not necessarily produce comparable valuation changes in the USDT operational balance.

The November 2024 market rally is used as the comparison case.

### Access-risk proposition

Price stability alone is not sufficient to determine whether the operational balance remains usable.

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

MODELLED OPERATIONAL BALANCE
USDT
    ↓
Did the balance remain stable and usable?

COMPARISON STABLECOIN
USDC
    ↓
Did another stablecoin behave differently?

RISK MECHANISM
    ↓
LUNA     → contagion / peg risk
Celsius  → counterparty / access risk
SVB      → reserve / banking infrastructure risk
Election → positive-market comparison
```

The exact quantitative analysis differs by event because each scenario represents a different risk mechanism.

---

## Core Metrics

For stablecoin valuation-risk cases, the main measures are:

- **Peg deviation** — how far the stablecoin moves from its intended $1 value.
- **Maximum negative peg deviation** — the lowest observed value within the event window.
- **Threshold persistence** — number of hourly observations below selected levels such as `$0.995`, `$0.990`, and `$0.980`.
- **Recovery time** — time required to return above a selected tolerance threshold after the lowest point.

These metrics are applied where they are relevant to the event rather than mechanically repeated in every case.

For the Celsius access-risk scenario, the analysis instead separates:

- **Market Value**
- **Available Operational Liquidity**
- **Availability Ratio**
- **Liquidity at Risk**

---

## Event Findings

### SVB / USDC

The SVB case showed that stablecoins can have very different risk profiles even under the same broader market conditions.

USDC reached an approximate implied value of **$0.8547**, around **14.53% below its intended $1 value**, while USDT remained comparatively stable.

USDC also showed substantially greater peg-stress persistence and required approximately **57 hours** from its lowest point to return above the $0.995 tolerance threshold.

For the modelled strategy, the USDT operational balance remained comparatively resilient during this event.

The USDC experience nevertheless demonstrates that **the choice of stablecoin and the infrastructure supporting its reserves can materially affect risk**.

### 2024 U.S. Election Rally

The post-election period provided a positive-market comparison rather than a crisis scenario.

BTC and ETH rose strongly during the selected period, while USDT and USDC remained broadly anchored around $1.

The analysis did not identify a clear asset-specific stablecoin shock associated with the rally.

For the modelled USDT operational balance, this means that the conversion reduced exposure to the strong upward movement in BTC and ETH as well as to potential downward movements.

The trade-off is **opportunity cost**: funds converted into USDT would not participate in subsequent BTC or ETH price gains.

### Cross-Event Interpretation

Together, the four cases show that stablecoin conversion changes the type of risk rather than eliminating risk entirely:

- **LUNA:** value can be affected by stablecoin contagion;
- **Celsius:** value can remain while access disappears;
- **SVB:** reserve infrastructure can create asset-specific stablecoin stress;
- **Election rally:** price stability also means giving up exposure to potential market upside.

---

## Key Terms

**Stablecoin**  
A crypto asset designed to maintain a stable value relative to another asset. USDT and USDC are designed to track the US dollar.

**Peg**  
The target value a stablecoin is designed to maintain. For USDT and USDC, the target is approximately $1.

**Depeg**  
A movement away from the intended stablecoin peg.

**Operational Balance**  
Funds held to support day-to-day payment activities such as payouts, settlements and liquidity needs. In this project, the modelled operational balance is held in USDT.

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

**Comparison Stablecoin**  
A stablecoin included in the analysis to help determine whether observed behaviour is specific to the modelled USDT balance or part of a broader stablecoin-market movement.

**Reserve Infrastructure**  
The cash, liquid assets, banks, custodians and other arrangements used to support the value and redeemability of a stablecoin.

**Opportunity Cost**  
The potential benefit given up when choosing one option instead of another. In this project, converting volatile crypto into USDT reduces exposure to both future losses and future gains.

---

## Data Sources

The project currently combines several public market-data sources:

- **yfinance** — daily BTC, ETH, USDT and USDC market data used for broader historical context.
- **Binance public API** — hourly BTC/USDT and ETH/USDT market data.
- **Coinbase Exchange API** — hourly USDT/EUR and USDC/EUR market data.
- **Dukascopy** — hourly EUR/USD FX data used to estimate approximate USD values for the Coinbase USDT/EUR and USDC/EUR market data.
- **Public event sources** — used to establish defensible event timelines and T0 reference points.

Raw and processed datasets are excluded from the repository and can be recreated through the project data-ingestion pipeline.

### Stablecoin Price Reconstruction

Historical stablecoin data used in the analysis is sourced from Coinbase EUR markets (`USDT/EUR` and `USDC/EUR`).

Because the project evaluates stablecoin stability relative to the $1 target, EUR-denominated prices are converted into approximate USD values using an independent EUR/USD benchmark:

`stablecoin/EUR × EUR/USD = approximate stablecoin/USD`

The resulting values should therefore be interpreted as **implied USD prices rather than direct USD-market observations**.

This introduces an additional methodological limitation: the stablecoin and FX prices come from separate market feeds with different liquidity, timestamp availability and trading schedules.

The limitation is particularly relevant during weekends, when crypto markets continue trading while the traditional FX market is closed. Where required, the most recent available EUR/USD observation is carried forward and explicitly flagged in the event analysis.

For this reason, small deviations from the $1 target should not automatically be interpreted as stablecoin-specific stress. The analysis considers the **magnitude, persistence and relative behaviour of USDT and USDC** when interpreting peg deviations.

---

## Project Structure

```text
stablecoin-settlement-resilience/
│
├── data/                       # excluded from Git
│
├──notebooks/
    ├── 01_data_ingestion.ipynb
    ├── 02_data_cleaning.ipynb
    ├── 03a_data_exploration_luna.ipynb
    ├── 03b_data_exploration_celsius.ipynb
    ├── 03c_data_exploration_svb.ipynb
    └── 03d_data_exploration_election.ipynb
│
├── .gitignore
└── README.md
```

The project will later include the SQL/dbt transformation layer and final Tableau outputs.

---

## Current Progress

- [x] Project scope and analytical framework revised
- [x] Data ingestion pipeline
- [x] Data cleaning and validation
- [x] LUNA event EDA
- [x] Celsius event EDA
- [x] SVB / USDC event EDA
- [x] November 2024 positive-market event EDA
- [ ] Cross-event comparison
- [ ] DuckDB + SQL/dbt transformation layer
- [ ] Final Tableau dashboard
- [ ] Final conclusions and operational recommendations

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
