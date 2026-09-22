# 🚀 Deployment ጋይድ (EthioAlibaba)

## አማራጭ 1 — PythonAnywhere (ለጀማሪዎች ቀላል, web upload = drag & drop አይነት)

1. https://www.pythonanywhere.com ላይ እርሁ (free account)
2. **Files** → Upload a file → `ethioalibaba.zip` ስቀል → Terminal ክፈት → `unzip ethioalibaba.zip`
3. **Web** → Add a new web app → Manual configuration → Python 3.10
4. Virtualenv: `mkvirtualenv venv --python=python3.10` ከዚያ `pip install -r requirements.txt`
5. WSGI configuration ፋይል ውስጥ:
   ```python
   import sys
   path = '/home/YOURUSERNAME/ethioalibaba'
   if path not in sys.path: sys.path.insert(0, path)
   from app import app as application
   ```
6. **Reload** ን ጫን → https://yourusername.pythonanywhere.com ይሰራል
7. Telegram webhook: `python app.py set-webhook https://yourusername.pythonanywhere.com`

## አማራጭ 2 — Render (free, GitHub አስፈላጊ)

1. ኮዱን GitHub ላይ push አድርግ (private repo)
2. https://render.com → New Web Service → repo ይምረጡ
   - Build command: `pip install -r requirements.txt`
   - Start command: `gunicorn app:app`
3. Environment variables ውስጥ: `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`, `SECRET_KEY`
4. Deploy ከማለቁ በኋላ: `python app.py set-webhook https://your-app.onrender.com`

⚠️ Render free tier sleep ይልላል — 24/7 ለማስነሳት paid ወይም PythonAnywhere ይጠቀሙ።
⚠️ SQLite on Render free = ዳታ ይጠፋል! PythonAnywhere (persistent disk) ይመከራል።

## 🔄 Telegram bot — deploy ላይ

- **Webhook mode**: public URL ማግኘት አለበት (PythonAnywhere/Render ሁለቱም ይሰጣሉ)
  → `python app.py set-webhook https://your-domain.com`
- **Polling mode**: URL አያስፈልግም → ሆኖም free tier sleep ስለሚል webhook ይሻላል

## 💳 ክፍያ (Telebirr) እንዴት እንደሚሰራ

**አሁን ያለው = MANUAL (በእጅ):**
1. Customer Telebirr → +251 91 234 5852 ገንዘብ ይላካል
2. በorder form "Telebirr Transaction ID" ይጽፋል
3. እርስዎ Telebirr appዎ ላይ TXN-ውን አረጋግጠው `/status ETHA1B2C3 Confirmed` ትላሉ
4. ቦቱ customer status ያሳያል

**Automated ለማድረግ:** Ethio Telecom Telebirr merchant API (business agreement) ያስፈልጋል — ይሄ የወደፊት እርምጃ ነው።

## 🤖 Customer Service ↔ Website ግንኙነት

- ሁለቱም **አንድ ዳታቤዝ** ይጠቀማሉ (ethioalibaba.db) — በwebsite የተጫነ order በቦት ይታያል
- Website (JS) ↔ Python (Flask API) ↔ Database ↔ Telegram bot
- Customer በቦት /track ORDER_ID ጽፎ status ያገኛል
- Customer ጥያቄ → AI auto-reply + copy ወደ እርስዎ (admin)
