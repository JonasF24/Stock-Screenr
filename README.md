# Personal Screener

A live, browser-based stock research dashboard built for identifying high-quality investment opportunities across three distinct strategies. Data is sourced in real time via the Finnhub.io API.

**Made by Jonas Flynn**

---

## Overview

Personal Screener is a single HTML file that runs entirely in your browser. It pulls live quotes, fundamentals, and news headlines directly from Finnhub and applies three independent stock screens to surface the best opportunities within each strategy. All screening criteria are verified against the most recent earnings reports.

---

## Features

- **Three independent screeners** — Low Risk Value, Buffett Stocks, and Dividend Growth
- **Live quotes** via Finnhub REST API with WebSocket real-time tick updates
- **Earnings-verified screening** — criteria checked against actual reported figures, not estimates
- **Insights panel** — per-stock investment thesis and risk factors on every passing name
- **Near-miss tables** — top 15 stocks that came closest to passing, with per-criterion breakdown
- **Post-Market News Feed** — auto-fetches headlines for any selected stock after 4:00 PM ET daily
- **Dark / Light mode** — toggle in the top right, preference saved across sessions
- **Dual clocks** — local time and US Eastern Time displayed simultaneously
- **ETF price strip** — live quotes for SCHD, SPY, VOO, and VTI as market benchmarks

---

## The Three Screens

### 1. Low Risk Value Screen

Targets businesses with consistent, above-average growth trading at a low price relative to their expected growth rate. Financial Services, Basic Materials, Energy, Utilities, and Real Estate sectors are excluded.

| Metric | Condition |
|---|---|
| Revenue Growth (5Y) | > 50% |
| Revenue Growth (1Y, TTM) | > 5% |
| Earnings Growth (1Y, TTM) | > 5% |
| Return on Equity (ROE) | > 15% |
| Debt to Equity | ≥ 0 and < 1 |
| Free Cash Flow (TTM) | > 0 |
| PEG Ratio (5Y Exp-Mean) | > 0 and < 1 |

**Passing stocks (as of March 2026):** NVDA, AVGO, MRVL, META

---

### 2. Buffett Stocks

Classic value-compounder criteria inspired by fundamental quality investing. Targets profitable businesses with strong returns on equity, conservative balance sheets, and growing dividends.

| Metric | Condition |
|---|---|
| Price to Earnings (PE) | 0 – 25 |
| Price to Book (PB) | 0 – 5 |
| Return on Equity (ROE) | > 20% |
| Debt to Equity | 0 – 0.5 |
| Free Cash Flow (TTM) | > 0 |
| Dividend Yield | > 0% |
| Revenue Growth (5Y) | > 20% |

**Passing stocks (as of March 2026):** TRV, GD, CSCO

---

### 3. Dividend Growth Stocks

Targets top-500 US companies by market cap that combine strong, consistent dividend growth with underlying business quality. Stocks are **ranked by dividend yield** (highest to lowest).

| Metric | Condition |
|---|---|
| Dividend Yield | > 1.5% |
| Dividend Growth | 5+ consecutive years of increases |
| Revenue Growth (5Y) | > 20% |
| Return on Equity (ROE) | > 15% |
| Debt to Equity | < 1 |
| Free Cash Flow (TTM) | > 0 |
| Payout Ratio | < 70% |

**Passing stocks (as of March 2026, ranked by yield):** QCOM, ADP, FAST, ACN, UNH

---

## How to Run

Because the Finnhub API enforces CORS restrictions, the file must be served from a local web server rather than opened directly from your file system.

**Option 1 — Python (recommended, no install required):**
```bash
cd ~/Downloads          # or wherever you saved the file
python3 -m http.server 8080
```
Then open `http://localhost:8080/finnhub-dashboard.html` in your browser.

**Option 2 — Node.js:**
```bash
npx serve .
```

**Option 3 — VS Code:**
Install the Live Server extension, right-click the HTML file, and select *Open with Live Server*.

---

## Post-Market News

The Post-Market News section automatically fetches the latest headlines for a selected stock after US market close (4:00 PM Eastern Time, Monday–Friday). You can also trigger it manually at any time using the **▶ Fetch Now** button.

- Select any ticker from the Low Risk Value, Buffett, or Dividend screens using the pill buttons
- Headlines display with timestamp, clickable source name, and clickable article title
- Auto-fetch runs once per session per day; preference is remembered until the page is refreshed

---

## Technical Details

- **Stack:** Plain HTML, CSS, and vanilla JavaScript — no frameworks, no build step
- **Data source:** [Finnhub.io](https://finnhub.io) free-tier API
- **Live prices:** WebSocket stream (`wss://ws.finnhub.io`) for real-time tick updates on passing stocks
- **Persistence:** Theme preference stored in `localStorage`; post-market fetch state in `sessionStorage`
- **Offline behavior:** If the API is unreachable, the screener displays skeleton loaders and shows a setup guide

---

## Disclaimer

This tool is for informational and research purposes only. Nothing displayed here constitutes financial advice. Always conduct your own due diligence before making any investment decision.

---

*Personal Screener · Made by Jonas Flynn*
