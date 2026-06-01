# Prosperity Scope

Trading analytics dashboard built for **IMC Prosperity 4**, a global algorithmic trading competition with over 22,000 participants.

**Live Demo:** https://prosperity-scope.vercel.app

Prosperity Scope transforms backtest logs into an interactive analytics dashboard, providing instant market microstructure insights including order book imbalance, Hurst exponent analysis, fill quality assessment, and P&L attribution — all computed directly in the browser.

---

## Features

### Price & Trades

* Mid-price tracking
* Bid/ask visualisation
* Fair value overlays
* EMA and Bollinger Bands
* Buy and sell execution markers

### P&L Curve

* Cumulative profit and loss tracking
* Drawdown visualisation
* Performance monitoring over time

### Market Microstructure Analytics

* Bid-ask spread analysis
* Order Book Imbalance (OBI)
* OBI correlation tracking

### Volume Profile

* Fill distribution across price levels
* Execution concentration analysis

### Trade Log

* Sortable table of all executed trades
* Detailed execution history

### Performance Metrics

* Final P&L
* Maximum drawdown
* Hurst exponent (market regime classification)
* Volatility
* Autocorrelation
* Average spread
* Fill statistics

---

## Supported Formats

The dashboard supports:

* Prosperity backtester `.log` files
* Prosperity submission `.json` files
* Lambda log arrays

All parsing and analytics are performed client-side.

---

## Getting Started

### 1. Open the Dashboard

Visit:

```text
https://prosperity-scope.vercel.app
```

### 2. Load a Sample Log

Download:

```text
sample/demo_run.log
```

from this repository and drag it directly onto the dashboard.

### 3. Generate Your Own Backtest

Install the included backtester:

```bash
pip install -e backtester/
```

Run the demo trader:

```bash
python -m prosperity4bt demo/trader_v1.py 0--1 0--2 --merge-pnl --out my_run.log
```

Then drag:

```text
my_run.log
```

onto the dashboard for analysis.

---

## Architecture

```text
index.html              Single-file dashboard
demo/
├── trader_v1.py        Demo trading algorithm
├── datamodel.py        Prosperity 4 type definitions

sample/
└── demo_run.log        Example backtest output
```

The entire application is contained within a single HTML file.

Technology stack:

* Vanilla JavaScript
* Plotly.js (CDN)
* No build process
* No framework dependencies

Analytics including log parsing, Hurst exponent calculation, FFT processing, and OBI correlation are executed entirely in-browser.

---

## Demo Trader

The repository includes a demonstration market-making strategy located in:

```text
demo/trader_v1.py
```

The trader is designed for the tutorial-round products:

### EMERALDS

Stable asset strategy featuring:

* Wall-mid fair value estimation
* Overbid and undercut quoting
* Aggressive liquidity taking when mispricing is detected

### TOMATOES

Mean-reversion strategy featuring:

* VWAP-based fair value estimation
* Inventory-aware position management
* Position skewing and soft inventory limits

The trader emits custom:

```text
SIG|
```

signal lines which the dashboard uses to render:

* Fair value overlays
* Bollinger Bands
* Order Book Imbalance visualisations

---

## Why Prosperity Scope?

Prosperity Scope was built to bridge the gap between raw backtest output and actionable trading insight.

Rather than manually inspecting logs, traders can immediately understand:

* Strategy profitability
* Execution quality
* Market regime behaviour
* Liquidity dynamics
* Order book structure

through a single interactive dashboard.
