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

## Using ChatGPT Instead

This project currently uses Google Gemini through `GOOGLE_API_KEY`.

If you want to use the ChatGPT API instead, switch the AI client in `index.js` from `GoogleGenerativeAI` to `ChatOpenAI`, then replace the Google environment variables with:

```env
OPENAI_API_KEY=
```

The OpenAI package is already included in `package.json`, and the starter ChatGPT code is commented in `index.js`.

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

## Deploying To Render

This repo includes `render.yaml` for Render Blueprint deploys.

To deploy:

1. Push the repo to GitHub.
2. In Render, create a new Blueprint from the GitHub repo.
3. Render will create the web service and database from `render.yaml`.
4. Add the secret values Render asks for, including Slack tokens and `GOOGLE_API_KEY`.

Do not commit `.env` or real token values. Keep local secrets in `.env` and production secrets in Render.
