# Slack AI Agent

A Node.js Slack bot that watches for new Slack members, gathers lightweight public context, analyzes fit with Google Gemini, stores the result in PostgreSQL, and posts a summary to a private Slack channel.

## Requirements

- Node.js 18+
- PostgreSQL database
- Slack app configured for Socket Mode
- Google AI API key

## Setup

Install dependencies:

```bash
npm install
```

Create your local environment file:

```bash
cp .env.example .env
```

Fill in `.env` with your own values. Keep `.env` private; it is intentionally ignored by git.

## Environment Variables

| Variable | Description |
| --- | --- |
| `DATABASE_URL` | PostgreSQL connection string. |
| `SLACK_BOT_TOKEN` | Slack bot token. |
| `SLACK_APP_TOKEN` | Slack app-level token for Socket Mode. |
| `SLACK_SIGNING_SECRET` | Slack app signing secret. |
| `SLACK_PRIVATE_CHANNEL_ID` | Channel where member analysis summaries are posted. |
| `GOOGLE_API_KEY` | Google AI API key used for Gemini analysis. |
| `GOOGLE_MODEL` | Gemini model name. Defaults to `gemini-2.5-flash`. |
| `COMPANY_NAME` | Company name included in the AI analysis prompt. |
| `COMPANY_PRODUCT` | Product name included in the AI analysis prompt. |
| `PORT` | Express server port. Defaults to `3000`. |
| `NODE_ENV` | Use `development` to enable the test endpoint. |

## Running

Start the app:

```bash
npm start
```

Run in watch mode during development:

```bash
npm run dev
```

When `NODE_ENV=development`, you can test analysis with:

```bash
POST http://localhost:3000/test/analyze-member
```

The health endpoint is available at:

```bash
GET http://localhost:3000/health
```

## GitHub Secrets

Do not commit `.env` or real token values. For GitHub Actions or deployment, add secrets in:

`Settings` -> `Secrets and variables` -> `Actions`

Then reference them from your workflow as needed.
