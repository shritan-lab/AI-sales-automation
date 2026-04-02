# AI Sales Automation

A fully self-hosted, production-ready sales automation system. Find leads, generate personalized AI emails, and send them via Gmail — all from one clean UI.

## Features

- **Lead Generation** — Real prospects via Vibe Prospecting (filtered by niche, seniority, company size, country)
- **AI Email Personalization** — Claude writes a unique cold email per lead
- **Gmail Sending** — Sends via your Gmail account using App Passwords (no OAuth setup needed)
- **Reply Qualification** — Paste any reply; AI classifies intent and tells you what to do
- **Campaign Analytics** — Track sent/failed, export to CSV

## Quick Start

### 1. Install dependencies
```bash
npm install
```

### 2. Configure environment
```bash
cp .env.example .env
```
Edit `.env` and fill in:
- `ANTHROPIC_API_KEY` — from [console.anthropic.com](https://console.anthropic.com/settings/keys)
- `GMAIL_USER` — your Gmail address
- `GMAIL_APP_PASSWORD` — generate at [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)

### 3. Start the server
```bash
npm start
```
Open [http://localhost:3000](http://localhost:3000)

## Gmail App Password Setup

1. Go to your Google Account → Security
2. Enable 2-Step Verification (required)
3. Go to [App Passwords](https://myaccount.google.com/apppasswords)
4. Create password: App = "Mail", Device = "Other" → name it "SalesBot"
5. Copy the 16-character password into `.env` as `GMAIL_APP_PASSWORD`

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/health` | Check all integrations |
| POST | `/api/leads` | Search prospects via Vibe Prospecting |
| POST | `/api/generate-email` | Generate personalized cold email |
| POST | `/api/send-email` | Send via Gmail SMTP |
| POST | `/api/qualify-reply` | Classify reply intent |

## Deploy to Production

### Railway (recommended — one click)
```bash
npm install -g @railway/cli
railway login
railway init
railway up
```
Add your env vars in the Railway dashboard.

### Render
- Connect your GitHub repo
- Set environment variables
- Deploy (auto-detects Node.js)

### VPS / DigitalOcean
```bash
# Install Node 18+
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Clone and run
git clone <your-repo>
cd ai-sales-automation
npm install
cp .env.example .env && nano .env
npm start

# Keep alive with PM2
npm install -g pm2
pm2 start server.js --name salesbot
pm2 startup && pm2 save
```

## Selling This Product

This is a white-label-ready sales automation tool. You can:

1. **White-label** — Change the name/logo in `public/index.html`
2. **Add auth** — Wrap with Passport.js or Clerk for multi-user SaaS
3. **Add database** — Connect MongoDB/Postgres to persist leads and campaigns
4. **Add billing** — Stripe integration for subscription plans
5. **Deploy per client** — Each client gets their own instance with their keys

### Suggested Pricing
- Solo license: $297 one-time
- Agency license: $97/month (unlimited campaigns)
- Done-for-you setup: $500 setup fee + $97/month

## Tech Stack

- **Backend**: Node.js + Express
- **AI**: Anthropic Claude (claude-sonnet-4)
- **Lead Data**: Vibe Prospecting via Claude MCP
- **Email**: Nodemailer + Gmail SMTP
- **Frontend**: Vanilla HTML/CSS/JS (no framework, fast load)

## File Structure

```
├── server.js          # Express backend + all API routes
├── public/
│   └── index.html     # Complete frontend UI
├── package.json
├── .env.example       # Config template
└── README.md
```
