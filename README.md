# 🥞 BNB PancakeSwap Quant 🤖

**Your Personal AI Quant for 5-minute PancakeSwap Prediction (BNB) rounds**.

This project is a Telegram bot powered by Google Apps Script that acts as your personal financial analyst. You can describe any trading strategy using **voice or text**, and the bot, using AI (Gemini & Groq Whisper), will automatically write the code, backtest it on historical data, and generate a detailed quantitative report.

## ✨ Key Features
* 🎙 **Voice Input:** Dictate your strategy idea in Telegram (using Groq Whisper for transcription).
* 🧠 **AI-Coding:** Gemini AI automatically translates your text description into executable JavaScript code for backtesting.
* 📊 **Deep Backtesting:** Instant simulation on historical PancakeSwap prediction rounds data.
* 📈 **Quantitative Analytics:** Calculation of WinRate, PnL, Profit Factor, Drawdowns, Sharpe and Sortino ratios, as well as serial analysis (Z-Score, Markov transitions).
* 🌍 **Multilanguage Support:** The bot fully supports 14 languages (English, Russian, Ukrainian, Spanish, French, German, Chinese, Turkish, Arabic, Italian, Portuguese, Hindi, Japanese, Korean) for natural communication and reporting.
* 🔒 **Privacy:** The bot works strictly individually and only responds to your specific `CHAT_ID`.

---

## 🚀 Installation and Deployment Guide (Step-by-Step)

You do not need a server. The project runs entirely on Google's free infrastructure (Google Sheets + Apps Script).

### Step 1. Create a copy of the database
1. Follow the link to the Google Sheets template: **[PancakeSwap Quant (Template)](https://docs.google.com/spreadsheets/d/1wmmgXLhIj2hRxWWPyx4ZrrU9ix_CcNG4NcTSOcTYCac/copy)**
2. Click the blue **"Make a copy"** button. *The entire bot source code will be copied to your Google Drive along with the spreadsheet.*

### Step 2. Get API Keys
You will need 3 keys and your Telegram ID to operate the bot:
1. **Telegram Bot Token:** Message [@BotFather](https://t.me/BotFather) on Telegram, create a new bot with the `/newbot` command, and copy the provided token.
2. **Your Chat ID:** Message [@userinfobot](https://t.me/userinfobot) or similar to find out your numeric ID. The bot will *only* reply to you.
3. **Groq API Key:** Register at [console.groq.com](https://console.groq.com/keys) and create a free API key (needed for voice message recognition).
4. **Gemini API Key:** Go to [Google AI Studio](https://aistudio.google.com/app/apikey) and create a key (responsible for code generation and analytics).

### Step 3. Configuration Setup
Open your copied Google Spreadsheet. Go to the **`data`** sheet.
Fill in the corresponding cells in column `B` with your data:
* Cell `B1` ➔ Token from BotFather
* Cell `B2` ➔ Your Telegram ID
* Cell `B3` ➔ Groq API Key
* Cell `B4` ➔ Google AI Studio API Key
* Cell `B5` ➔ *(Optional)* Decimal places for reports (default is 4).

### Step 4. Publish Webhook (Deploying the script)
To allow Telegram to send messages to your script, you need to publish it as a web app:
1. In the top menu of Google Sheets, click `Extensions` ➔ `Apps Script`.
2. In the code editor that opens, click the blue **Deploy** button in the top right corner ➔ **New deployment**.
3. Select type: **Web app**.
4. Access settings:
   * Execute as: **Me**.
   * Who has access: **Anyone**.
5. Click **Deploy**. On the first run, Google will ask for permissions — agree to everything.
6. A window with a **Web app URL** will appear at the end. Copy it!

### Step 5. Link Webhook and Commands
Return to Google Sheets to the **`data`** sheet:
1. Paste the **Web app URL** copied in the previous step into cell **`B6`**.
2. Click the link in cell **`A6`** (`linkApp 🔥 set WEBHOOK`) and follow it. You should see a Telegram message in the browser: `{"ok":true,"result":true,"description":"Webhook was set"}`.
3. Click the link in cell **`A7`** (`📋 Setup Commands`) and follow it. This will add a convenient command menu to your bot. The browser will show `{"ok":true,"result":true}`.

🎉 **Done! Go to your bot in Telegram and send it a voice or text message with a strategy idea.**

---

## 🛠 Usage Examples & Supported Prompts

You can speak or type to the bot in any of the 14 supported languages to dictate complex logic. Here are some examples of what the bot can understand and process:

**Trend-Following Strategy:**
> "Let's check a reversal strategy. If the previous round closed with an uptrend (bull), we bet on a downtrend (bear). If it was a downtrend, we bet on an uptrend."

**Streak / Martingale Evaluation:**
> "Test a strategy where we only enter a trade after 3 consecutive BULL rounds, and we bet BEAR. Stop after 1 win."

**Odds-Based Strategy:**
> "If the payout multiplier (odds) for BULL is greater than 2.0, and the previous round was BEAR, place a bet on BULL."

**The Bot's Response (Markdown file):**
The bot will generate the code, run a backtest on the built-in history, and provide a detailed document:
* **Winrate, PnL, Profit Factor.**
* **Streak Analysis:** Maximum consecutive wins/losses.
* **AI Mathematical Report:** Explanation of autocorrelation, probabilities like `P(Win|Win)`, and recommendations for adding filters (e.g., skip trades with odds below 1.85).

---

## ⚙️ Bot Commands
* `/start` - Check the bot's status.
* `/clear` - Clear the chat history (useful if the AI gets confused by previous versions of a strategy).
* `/history` - Download the current built-in PancakeSwap round history in `.json` format.

## ⚠️ Limitations
* The bot replies strictly to the user whose `CHAT_ID` is specified in the settings.
* The daily query quota is limited by Gemini API free limits (if the bot throws a quota error, just wait for the daily reset).
