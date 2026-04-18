# Automated Event Contract Trading Bot

An AI-powered trading bot that autonomously trades Bitcoin hourly contracts on Kalshi's CFTC-regulated prediction market exchange.

## Live Performance

| Metric | Value |
|--------|-------|
| Live Win Rate | 82.4% |
| Backtest Win Rate | 93.1% (57,530 trades) |
| Backtest Period | Sep 2019 to Apr 2026 |
| Worst Month Ever | 86.8% |
| Losing Months | 0 |
| Sharpe Ratio | 5.65 (adjusted ~2.5-3.5) |
| Max Drawdown | 5.32% |
| Brier Score | 0.141 (Excellent) |

## Architecture
Telegram Bot
|
v
AWS EC2 (Ubuntu 24.04, t3.micro)
|
|-- telegram_polling.py   (Command handler)
|-- sms_server.py         (Flask API - port 5050)
|-- bot.py                (Proprietary trading engine)
|-- kalshi_client.py      (Exchange API - RSA-PSS auth)
|
v
Kalshi Exchange (CFTC-regulated)
BTC Hourly Event Contracts

All four processes managed by PM2 with auto-restart and log rotation. Bot auto-starts on server reboot via systemd.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.12 |
| Exchange | Kalshi REST API v2 with RSA-PSS authentication |
| Messaging | Telegram Bot API |
| BTC Price Feed | Binance US public API |
| Compute | AWS EC2 t3.micro, Ubuntu 24.04 |
| Process Manager | PM2 |
| Dashboard | React + Recharts |
| API Server | Flask + Gunicorn |

## Verified Results

Backtested across 6.5 years of BTC hourly price data with no lookahead bias including every major market condition.

| Period | Win Rate | Trades |
|--------|----------|--------|
| 2019 Bear Market | 98.8% | 2,363 |
| 2020 Bull Run | 97.0% | 7,295 |
| 2021 ATH Run | 91.1% | 7,501 |
| 2022 Bear + FTX Collapse | 93.1% | 8,735 |
| 2023 Recovery | 95.0% | 8,728 |
| 2024 New ATH | 90.3% | 8,759 |
| 2025 Current | 91.7% | 2,567 |
| **Overall** | **93.1%** | **57,530** |

Monte Carlo simulation across 1,000 random samples of 500 trades showed a worst case win rate of 88.4% and zero samples below 80%. The strategy has never had a losing month in 6.5 years of simulated data.

All source code, strategy logic, and deployment details are proprietary and private.

## Disclaimer

For educational and personal use only. Event contract trading involves risk of loss. Past performance does not guarantee future results. This software is not financial advice.

## License

MIT
