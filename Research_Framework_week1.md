# Stablecoin Settlement Resilience

### Historical Stress Testing of Operational Crypto Balances Across Market, Counterparty, and Banking Shocks

## 1. Business Context

This project models a crypto payment operation in which volatile crypto assets are converted into **USDT or USDC** as a balance-management control to reduce direct exposure to BTC and ETH price volatility.

The conversion can reduce direct market-price exposure, but it does not eliminate operational risk. Stablecoin-denominated balances may still be affected by **peg instability, counterparty access restrictions, issuer and reserve exposure, banking dependencies, and liquidity conditions**.

The project therefore treats stablecoin conversion not as a final risk solution, but as a control whose resilience can be tested under different historical stress events.

The analysis is designed as a **historical stress-testing framework for operational crypto balances** rather than a trading model or a prediction model.

## 2. Business Question

> **When does holding operational balances in stablecoins effectively reduce exposure to crypto-market volatility, and under what conditions does the stablecoin or the infrastructure around it become a source of operational risk?**

The analysis separates two core layers:

**Market stress layer — BTC & ETH**

BTC and ETH are used as indicators of the severity, timing, and direction of the broader cryptocurrency market environment around each event.

**Operational balance layer — USDT & USDC**

USDT and USDC represent assets that may be used for operational liquidity. Their behaviour is evaluated to determine whether a stablecoin-denominated balance remains both **valuable and usable** during stress.

A key distinction developed through the project is:

> **Market value is not the same as operational liquidity.**

A balance may retain its observable market value while becoming inaccessible for payments or settlements.

## 3. Stress Scenarios

| Event | Risk mechanism | Main analytical question |
| --- | --- | --- |
| **LUNA / UST collapse — May 2022** | Stablecoin contagion / peg risk | Can the failure of another major stablecoin create measurable valuation stress in USDT or USDC? |
| **Celsius withdrawal halt — June 2022** | Counterparty / access risk | Can a stablecoin balance retain market value while becoming unavailable for operational use? |
| **SVB collapse / USDC depeg — March 2023** | Reserve / banking infrastructure risk | What happens when a banking shock directly affects reserves supporting a settlement stablecoin? |
| **Trump election win — November 2024** | Positive market-wide shock | Do USDT and USDC remain stable during a strong bullish crypto-market movement? |

The four events are intentionally different. The objective is not to rank events by severity, but to test how the same balance-management strategy behaves under **different failure mechanisms**.

## 4. Operational Balance Framework

The project uses hypothetical stablecoin-denominated operational balances to translate market movements into business-relevant liquidity impact.

Where a balance scenario is required, the baseline is expressed directly in stablecoin units, for example:

> **100,000 USDT operational balance**

The balance can then be translated into its observed **EUR market value** using the relevant stablecoin/EUR market price. This keeps the asset exposure intuitive while providing a fiat value that is easier to interpret in a European payments context.

BTC and ETH are not treated as the operational balance. They represent the **market environment**, while USDT and USDC represent the **balance exposure**.

The exact balance analysis depends on the risk mechanism of each event rather than forcing every event into an identical model.

## 5. Risk Dimensions and Metrics

### 5.1 Market stress

BTC and ETH daily and hourly returns are used to establish whether the event occurred during a stable, deteriorating, or rapidly moving crypto market.

Core observations include:

- daily price and return behaviour;
- hourly price and return behaviour around the event;
- largest negative or positive movements within the selected window;
- relationship between market stress and the externally defined event timestamp.

Market data are used for **context and timing**, not to claim causality by themselves.

### 5.2 Stablecoin valuation risk

For events where stablecoin price behaviour is the relevant mechanism, the analysis uses:

**Implied USD value**

Where the available stablecoin market is quoted in EUR, its implied USD value is derived using the EUR/USD benchmark:

$$
Stablecoin/USD_t = Stablecoin/EUR_t \times EUR/USD_t
$$

**Peg deviation**

$$
PegDeviation_t = (Price_t - 1) \times 100
$$

**Maximum negative peg deviation**

The lowest observed stablecoin value within the event window, used to capture worst observed valuation stress.

**Threshold persistence**

Time spent below analytical monitoring levels such as:

`$0.995` → `$0.990` → `$0.980`

This distinguishes a short-lived price movement from persistent peg stress.

**Recovery time**

Time required after the lowest observed value for the stablecoin to recover above the selected monitoring threshold.

### 5.3 Operational liquidity / access risk

Price data alone cannot determine whether funds are actually available for payments or settlements. For access-risk events, the framework therefore distinguishes:

**Market Value** — the observable fiat-equivalent value of the stablecoin balance.

**Available Operational Liquidity** — the portion of that value that can actually be accessed and used operationally.

**Availability Ratio**

$$
AvailabilityRatio_t = \frac{AvailableValue_t}{MarketValue_t}
$$

**Liquidity at Risk**

$$
LiquidityAtRisk_t = MarketValue_t - AvailableValue_t
$$

For the Celsius case, the withdrawal halt is modelled as a deterministic stress scenario in which availability changes from **100% before T0 to 0% after T0** for a hypothetical balance held on the affected platform. This is a scenario assumption, not an estimate of a specific historical Celsius account.

## 6. Research Hypotheses and Risk Propositions

### H1 — Market-volatility protection

> USDT and USDC will show substantially smaller price deviations than BTC and ETH during broad cryptocurrency market shocks.

If supported, this indicates that stablecoin conversion can reduce direct exposure to BTC/ETH price volatility within the modelled operation.

### H2 — Stablecoin contagion

> The failure of another major stablecoin may create temporary peg stress in USDT and/or USDC even without direct issuer exposure.

The **LUNA / UST collapse** is the main test case.

### H3 — Direct reserve / banking exposure

> A shock affecting the banking or reserve infrastructure supporting a stablecoin can produce materially greater peg instability than general cryptocurrency market volatility alone.

The **SVB / USDC event** is the main test case.

### H4 — Positive-market resilience

> Stablecoin price stability should remain materially stronger than BTC/ETH price movement during a broad positive crypto-market shock.

The **Trump election event** provides a positive-market comparator rather than another crisis scenario.

### Risk proposition — Counterparty and access risk

> **A stablecoin can retain its market value while losing its operational usefulness if the venue holding the balance restricts access to funds.**

The **Celsius withdrawal halt** tests this proposition through an operational liquidity stress scenario rather than through peg behaviour alone.

## 7. Event-Specific Analytical Framework

The project uses a common starting structure while allowing the final risk analysis to reflect the mechanism of each event.

```text
1. MARKET CONTEXT
   BTC / ETH daily analysis
        ↓
   BTC / ETH hourly analysis
        ↓
   What was happening in the broader crypto market?

2. EVENT DEFINITION
   External event timeline
        ↓
   T0 reference point
        ↓
   Where does the event sit within the observed market stress?

3. OPERATIONAL BALANCE RISK
        ↓
   Event-specific analysis

   LUNA
   → USDT / USDC peg deviation
   → threshold persistence
   → recovery

   CELSIUS
   → 100,000 USDT stress scenario
   → market value vs available liquidity
   → availability ratio
   → liquidity at risk

   SVB
   → USDC reserve / banking shock
   → peg severity and persistence
   → operational balance impact

   TRUMP
   → positive-market comparator
   → stablecoin resilience during bullish stress

4. CASE CONCLUSION
        ↓
   Which risk was reduced?
   Which risk remained?
   Which new risk became operationally relevant?
```

The framework deliberately avoids forcing every event into identical metrics when the underlying risk mechanism is different.

## 8. Findings to Date

### LUNA / UST collapse

The LUNA case shows that conversion from volatile crypto assets into stablecoins can reduce direct BTC/ETH market exposure without eliminating valuation risk.

During the selected event window, USDT experienced a material temporary deviation from its peg, reaching an implied USD minimum of approximately **$0.9716 (-2.84%)**. It remained below the `$0.995` monitoring threshold for **13 consecutive hourly observations**, including **7 observations below $0.990** and **2 below $0.980**. USDC showed substantially lower stress and did not breach the `$0.995` threshold.

The case therefore demonstrates **stablecoin-specific valuation and contagion risk** and shows that different stablecoins can behave differently during the same market shock.

### Celsius withdrawal halt

The Celsius case shows that price stability and operational availability are separate dimensions of risk.

BTC and ETH were already under substantial market stress before the withdrawal halt and remained volatile afterward. The withdrawal halt is therefore treated as a clearly observable **operational event**, not as the assumed beginning of the broader crypto sell-off.

For a hypothetical **100,000 USDT** balance, the first hourly market observation after the halt valued the balance at approximately **€95.2k**. Under the deterministic Celsius stress scenario, available operational liquidity falls to **€0**, while the same balance on an unaffected accessible venue remains usable at its observed market value.

The case therefore demonstrates **counterparty and access risk**: a balance can remain market-valued while becoming unavailable for payments or settlements.

### SVB / USDC

**Analysis in progress.** This case will test how a banking shock affecting stablecoin reserve infrastructure is transmitted into USDC peg behaviour and operational balance value.

### Trump election

**Pending.** This event will serve as the positive-market comparison case and test whether stablecoin resilience differs during a strong upward crypto-market movement.

## 9. Interpretation Boundaries

The project is a historical stress-testing framework, not a production risk model.

It does **not** attempt to:

- predict future stablecoin failures;
- prove that one stablecoin is universally safer than another;
- establish causality from price movements alone;
- estimate actual customer or company balances held during historical events;
- model every source of settlement risk such as order-book depth, slippage, blockchain congestion, redemption capacity, or real-time counterparty concentration.

Instead, the objective is to identify **which risks stablecoin conversion reduces, which risks remain, and which risks may not be visible through price monitoring alone**.

## 10. Technology and Project Pipeline

**Python / Jupyter** — API extraction, cleaning, validation, event research, exploratory analysis, and stress-scenario development.

**DuckDB** — local analytical database for consolidated market and event data.

**SQL + dbt Core** — transformation of cleaned data, standardisation of event-level metrics, and creation of reusable analytical datasets.

**Tableau** — final comparison of events, risk mechanisms, stablecoin behaviour, operational balance impact, and key risk indicators.

The intended workflow is:

```text
Raw market data
      ↓
Cleaning & validation
      ↓
Event-level EDA
      ↓
Standardised analytical models (SQL / dbt)
      ↓
Cross-event comparison
      ↓
Tableau risk view
```

## 11. Current Project Status

**Completed:**

- data collection and cleaning for the selected event datasets;
- LUNA event EDA and stablecoin peg-stress analysis;
- Celsius event EDA and operational liquidity stress scenario.

**Current:**

- SVB / USDC event exploration.

**Next:**

- Trump positive-market comparison;
- cross-event metric standardisation;
- DuckDB / dbt modelling;
- final comparative Tableau dashboard and conclusions.
