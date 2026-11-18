# Autonomous AI Paper-Trading Research Engine (n8n + Gemini)

An end-to-end automated market analysis and paper-trading engine built with **n8n**, **Google Gemini 2.5 Flash**, and **Telegram**. The system fetches live simulated market candles, calculates technical indicators, parses real-time financial news sentiment, and executes automated BUY/SELL decisions with instant Telegram alerts and daily performance scorecards.

## Architecture & Workflow

1. **Market Data & Portfolio Ingestion:** Scheduled trigger polls `/api/candles` and `/api/portfolio` endpoints for real-time price action and open position status.
2. **News Sentiment Aggregation:** Fetches top market headlines via RSS feeds (Economic Times Markets) and formats them into a unified context block.
3. **Technical Indicator Engine (JavaScript):** Computes **EMA (9 & 21)**, **MACD**, **RSI (14)**, and volume status directly inside an n8n Code node.
4. **AI Decision Engine (Gemini 2.5 Flash):** Evaluates technical setups, risk parameters (1.5% Stop-Loss / 3% Take-Profit), and news sentiment to output structured JSON signals (`BUY`, `SELL`, or `HOLD`).
5. **Automated Order Execution & Routing:** Routes decisions via an n8n Switch node to execute market orders (`/api/trade`).
6. **Telegram Live Alerts & Daily Scorecard:** Sends instant trade execution alerts with AI reasoning and generates an automated end-of-day PnL and win-rate summary.

## Tech Stack
* **Orchestration:** n8n (Cloud / Self-hosted)
* **AI Model:** Google Gemini 2.5 Flash (Structured JSON Output)
* **Data & Indicators:** JavaScript (Custom EMA, RSI, MACD computation), RSS Feeds
* **Notifications:** Telegram Bot API
* **Execution Backend:** RESTful Paper-Trading Simulator API

## Setup Instructions
1. Import the workflow JSON file into your n8n workspace.
2. Configure your credentials in n8n:
   * **Google Gemini Chat Model** (API Key or n8n Gateway)
   * **Telegram Bot API** (Bot Token from `@BotFather`)
3. Update the placeholder values in the HTTP Request and Telegram nodes:
   * `YOUR_SIMULATOR_URL`
   * `YOUR_SIMULATOR_API_KEY`
   * `YOUR_TELEGRAM_CHAT_ID`
4. Activate the workflow to run autonomously on schedule.
5.
