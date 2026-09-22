# EthioAlibaba — Organized Project

## Structure (andnet)
    ethioalibaba/
    ├── app.py              # ← Mulu backend ANDAND: website + API + Telegram bot
    ├── templates/
    │   ├── index.html      # Home page (login modal + order + track)
    │   └── register.html   # Full login / register page
    ├── requirements.txt
    └── .env (optional)

## Run (megbat)
    pip install -r requirements.txt

    python app.py               # Website only  → http://127.0.0.1:5000
    python app.py bot           # Telegram bot only (polling, no URL needed)
    python app.py all           # Website + Bot TOGETHER  ← recommended
    python app.py set-webhook https://yourdomain.com

## Telegram (anda section)
All bot logic is in app.py → section "TELEGRAM ADMIN BOT".
Bot commands work the SAME in webhook and polling mode:
    /track ETHA1B2C3   /orders   /status ETHA1B2C3 Shipped   /help

## Database
SQLite — `ethioalibaba.db` auto-creates on first run.
Tables: users, orders, status_history

## Login flow (index ↔ register)
• index.html modal → POST /api/login & /api/register (token in localStorage)
• /register page  → same APIs, redirects to /
• "My Orders" only works with token (Bearer)

## Security notes
• Change SECRET_KEY and move TELEGRAM_BOT_TOKEN / TELEGRAM_CHAT_ID to .env
