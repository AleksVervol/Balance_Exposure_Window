# Project Title

**Balance Exposure Window: Estimating Settlement Risk from Crypto Price Shocks**

## Short Description

This project looks at how long a payment operation could be exposed to financial risk after a major cryptocurrency price shock.

Using historical BTC and ETH price data, I simulate a **$100,000 crypto-denominated balance** and measure how its value could change if settlement takes **24, 48, or 72 hours**.

The analysis focuses on three major market shocks with different underlying causes:
- **Terra/LUNA collapse** (May 2022) — a crypto-native stablecoin failure
- **Celsius Network withdrawal halt** (June 2022) — a liquidity/exchange access disruption
- **Signature Bank closure** (March 2023) — a fiat-rail/banking disruption affecting the crypto industry

Comparing these three event types shows that not all shocks affect crypto-denominated balances the same way — some are driven by crypto market mechanics, others by the surrounding banking infrastructure.

The model also considers an important real-world payment constraint: **crypto markets operate 24/7, but fiat settlement does not**. If a major price move happens outside banking hours, such as during a weekend or holiday, the balance may remain exposed until the fiat settlement process resumes.

This reflects a real payment-operations problem: **the longer a balance stays unsettled during a volatile market, the greater the potential financial risk.**

### Data sources
- **yfinance** — daily BTC-USD and ETH-USD prices, 2020–2026 (baseline + event windows)
- **Binance public API** — hourly BTC-USDT and ETH-USDT prices for the ~30-day window around each of the three events
- **News/Wikipedia timelines** — used only to establish accurate event dates for LUNA, Celsius, and Signature Bank (not as a data source for prices or metrics)