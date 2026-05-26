# HR Interview Agent

A lightweight web app that generates thoughtful, role-specific interview questions using Google Gemini 2.5 Flash.

## Features

- Enter any job title to get 3 insightful interview questions tailored to that role
- AI-powered input validation — rejects non-job-title inputs and prompt injection attempts
- Rate limited to 20 requests per 15 minutes per client
- Automatic retries with exponential backoff on API failures
- Responsive UI built with Tailwind CSS

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js v24 |
| Server | Express 5 |
| AI | Google Gemini 2.5 Flash |
| Validation | Zod |
| Rate limiting | express-rate-limit |
| Frontend | Vanilla JS + Tailwind CSS CDN |

## Getting Started

### 1. Get a free Gemini API key

Go to [aistudio.google.com](https://aistudio.google.com), sign in with Google, and click **Get API key**. No credit card required.

### 2. Configure environment

Create a `.env` file in the project root:

```
GEMINI_API_KEY=your_api_key_here
PORT=3000
```

### 3. Install dependencies

```bash
npm install
```

### 4. Start the server

```bash
npm start
```

The app will be available at `http://localhost:3000`.

## Project Structure

```
hr-interview-agent/
├── server.js        # Express server, API routes, Gemini integration
├── public/
│   └── index.html   # Frontend UI
├── .env             # Environment variables (not committed)
└── package.json
```

## API

### `POST /api/get-questions`

Generates 3 interview questions for a given job title.

**Request body**
```json
{ "role": "Software Engineer" }
```

**Response**
```json
{
  "questions": [
    "Question 1",
    "Question 2",
    "Question 3"
  ]
}
```

**Validation errors** return `400`. AI/network failures return `502`. Invalid inputs (non-job-titles) return a single-item array with an error message.
