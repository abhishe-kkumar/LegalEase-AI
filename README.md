# LegalEase AI

LegalEase AI is a single-page Indian legal-information platform. It combines a searchable client-side law library with Gemini-powered explanations, scenario guidance, document drafts, quizzes, and legal-news features.

> LegalEase AI provides general information, not legal advice. AI output can be incomplete or inaccurate—verify important information with official sources and consult a qualified lawyer or emergency authority when needed.

## Features

- Browse and search Indian laws across criminal, civil, cyber, family, corporate, tax, and constitutional topics
- Ask questions from the home page, learning hub, help centre, or emergency guidance flow
- Generate plain-language law explanations and analyze legal scenarios
- Draft common legal documents using guided prompts
- Take legal knowledge quizzes, with a built-in fallback quiz if AI is unavailable
- Bookmark laws, track recently viewed items and XP, save news, select a theme, and store a display name locally in the browser
- Explore AI-generated legal news, case-law summaries, and daily tips

## Tech stack

- Static frontend: HTML, CSS, and vanilla JavaScript
- Backend: Node.js and Express
- AI: Google Gemini API

## Run locally

### Prerequisites

- Node.js 18 or later
- A Google Gemini API key (optional for browsing the built-in law library; required for AI features)

### Installation

```bash
npm install
```

Create a `.env` file in the project root:

```env
GEMINI_API_KEY=your_gemini_api_key
```

Start the application:

```bash
npm start
```

Then open [http://localhost:3000](http://localhost:3000).

For development with automatic server restarts:

```bash
npm run dev
```

## API key options

The app supports two ways to enable Gemini:

1. **Server key (recommended):** Set `GEMINI_API_KEY` in `.env`. The frontend sends requests to the local `/ai` endpoint, and the server communicates with Gemini.
2. **Browser key:** Use the in-app **API** button to add a key. It is stored in that browser's `localStorage` and requests are sent directly from the browser to Gemini.

Do not commit `.env` or share an API key. The server-side option is generally safer because it does not expose the key to browser users.

## Endpoints

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/health` | Returns service status and whether a server Gemini key is configured. |
| `POST` | `/ai` | Sends a prompt to Gemini. Accepts JSON with `prompt` and an optional `mode`. |

Example request:

```bash
curl -X POST http://localhost:3000/ai \
  -H "Content-Type: application/json" \
  -d '{"prompt":"What is Article 21?","mode":"general"}'
```

## Project structure

```text
├── index.html   # Application layout and UI content
├── styles.css   # Responsive styling
├── script.js    # Law data, UI behavior, browser storage, and AI requests
├── server.js    # Express server, static hosting, and Gemini proxy
├── package.json # Scripts and dependencies
└── .env         # Local Gemini key; keep private
```

## Notes

- The app serves all static files from the project root on port `3000`.
- User preferences, bookmarks, quiz data, and saved news are stored only in browser `localStorage`.
- The legal database and AI responses should be reviewed and kept current before using the application in a public or professional setting.
