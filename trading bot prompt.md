# trading bot prompt

I want to create an OpenClaw trading-advice agent for crypto markets. It should include:

1. Tools for market data ingestion using free-tier APIs where available, prioritizing CoinGecko, CoinMarketCap, and TradingView-compatible data, with fallback handling and rate-limit awareness.
2. Skills for analyzing uploaded context from William O’Neil, Mark Minervini, and my past crypto ChatGPT chats, extracting reusable trading rules, watchlist criteria, risk rules, and setup patterns.
3. Product behavior that gives structured trading advice only: market summary, setup quality, entry/exit zones, invalidation level, risk/reward, confidence score, and “not financial advice” disclaimer.

Ensure to use best practices. Double check the already existing code. Changes to other parts of the code must not be made without permission.

Use red/green test driven development.

# checklist

### python 
- module lives at `workspace/<name>/` — always invoke with `pythonpath=/path/to/workspace`
- never use system python. always call `.venv/bin/python` explicitly:
  ```
  pythonpath=/users/snappo/.openclaw/workspace \
  /users/snappo/.openclaw/workspace/<name>/.venv/bin/python -c "..."
  ```
- test import works before wiring cron: `from <name>.cli import health_check`

### agent SOUL.md
- `agentdir` soul.md is not always surfaced as primary context in cron-isolated sessions
- workaround: embed the bash invocation pattern directly in the cron message payload — don't rely on soul.md being loaded
- put pythonpath + venv path in soul.md anyway for human reference, but don't depend on it

### telegram cron delivery
- agents without an explicit telegram binding need `--to <chatid> --best-effort-deliver` in the cron payload
- verify `lastrunatms` appears in `jobs.json` after first fire — absence means the job never ran
- check `runs.sqlite` for execution history if output is missing

### git and ssh
- passphrase-protected deploy keys can't be unlocked headlessly — must run `ssh-add` interactively before any push in a new shell session
- always check `git status` before assuming a push succeeded

### validation seq
1. `health_check()` — confirms data fetch works
2. `analyze_coin('btc')` — confirms analysis pipeline end-to-end
3. manual cron trigger — confirms delivery before scheduling
4. check `jobs.json` after first scheduled window — confirms scheduler picked it up
