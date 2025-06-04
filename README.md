# AI-Powered Stock Trading Simulation Platform

A modular, agentic trading simulator where AI agents mimic real-world investor strategies and execute trades based on live market data, research tools, and persistent memory.

---

## 🚀 Features

- **Agent-Based Trading**: Simulates traders like Warren Buffett, Ray Dalio, George Soros, and Cathie Wood.
- **Real-Time & EOD Market Data**: Integrates with the Polygon API for real or delayed stock prices.
- **Research Agent**: Nested LLM researcher with Brave search, web fetch, and memory.
- **Autonomous Execution**: Agents make decisions, execute trades, send push updates, and self-log.
- **Live Dashboard**: View trader performance via a real-time Gradio UI.
- **SQLite Persistence**: Accounts, transactions, logs, and market data stored persistently.
- **Modular Microservices**: MCP-based server tools for accounts, markets, research, and push notifications.

---

## 🏁 Getting Started

1. Clone the repository and install the requirements.
2. Launch the MCP servers configured in `mcp_params.py`.
3. Create a `.env` file with your API keys. In addition to the Polygon and Pushover values, include keys for any LLM providers you plan to use:
   `OPENROUTER_API_KEY`, `DEEPSEEK_API_KEY`, `GOOGLE_API_KEY`, `GROK_API_KEY`, `ALPHA_VANTAGE_API_KEY`, `SMITHERY_API_KEY`.
4. Start the dashboard with `python app.py`.

---

## 🧱 Architecture Overview

- `trading_floor.py` — Main loop, launches and schedules traders
- `traders.py` — Trader class definition, model setup, and decision logic
- `accounts.py` — Account logic (buy, sell, PnL, strategy)
- `market.py` — Share price engine using Polygon API
- `push_server.py` — Push notifications using Pushover
- `alpha_client.py` — Connects to Smithery (optional external research)
- `templates.py` — Prompt instructions for traders and researchers
- `database.py` — SQLite layer for accounts, logs, and market history
- `app.py` — Gradio dashboard with charts and logs

---

## 🔧 Tool Server Configuration

| Server   | Script                              | Purpose               |
| -------- | ----------------------------------- | --------------------- |
| Market   | `market_server.py` or `mcp_polygon` | Share prices          |
| Accounts | `accounts_server.py`                | Trading actions       |
| Push     | `push_server.py`                    | Notifications         |
| Research | `brave-search`, `fetch`, `memory`   | News and memory tools |

Launch configuration is controlled via `mcp_params.py`

---

## 🧠 How It Works

1. Scheduler loop starts and checks market status.
2. Each trader agent is launched with their own persona and model.
3. The agent receives account + strategy context, performs research, and executes trades.
4. Tools are invoked via subprocess (MCP protocol): `buy_shares`, `lookup_share_price`, etc.
5. Logs and transactions are saved and visualized in real-time.
6. Push notifications summarize each trade session.

---

## 🖥️ Dashboard

To run the Gradio UI:

```bash
python app.py
```

- View live holdings, transactions, PnL
- Logs update every 0.5 seconds
- Charts update every 2 minutes

---

## ⚙️ Environment Variables

Set in `.env`:

```
POLYGON_API_KEY=...
POLYGON_PLAN=paid / realtime / free
PUSHOVER_USER=...
PUSHOVER_TOKEN=...
BRAVE_API_KEY=...
OPENROUTER_API_KEY=...
DEEPSEEK_API_KEY=...
GOOGLE_API_KEY=...
GROK_API_KEY=...
ALPHA_VANTAGE_API_KEY=...
SMITHERY_API_KEY=...
USE_MANY_MODELS=true / false
RUN_EVERY_N_MINUTES=30
RUN_EVEN_WHEN_MARKET_IS_CLOSED=true / false
```

LLM provider keys and `ALPHA_VANTAGE_API_KEY` are optional but required if you
plan to use those models or the Alpha Vantage tools.

---

## 📦 Dependencies

- `gradio`
- `polygon` (SDK)
- `pydantic`
- `openai`, `asyncio`, `uv`
- `mcp` (Model Context Protocol)
- `sqlite3`

---

## 🧪 Development Notes

- Reset trader state: `python reset.py`
- Extend with new personas in `reset.py`
- Add new tools using `FastMCP`
- Customize prompts in `templates.py`

---

## 🧵 Credits

Project created under the guidance of **Ed Donner** as part of an advanced exploration of agent-based systems and LLM-powered tool use.

---

## 📬 Contact

Happy to collaborate or share more! Let’s build smarter agents. 🧠

#AI #OpenAI #Polygon #StockTrading #AgenticAI 
