# BackEnd API — Legacy.Ai

This document describes the BackEnd Express API for the Legacy.Ai project and how the Gemini generative model (via the Google Generative AI client) is used.

## Overview

- Language: Node.js + Express
- Entry point (for app wiring): `src/app.js`
- Routes: `src/routes/ai.routes.js`
- Controller: `src/controllers/ai.controller.js`
- Service that calls the Gemini model: `src/services/ai.service.js`

## Available Endpoints

All routes are mounted under the `/ai` prefix (see `src/app.js`).

1) POST /ai/get-review

  - Description: Send source code (or any text prompt) to the AI code-reviewer service. The service forwards the prompt to the Gemini generative model and returns the model's text output.
  - Request body (JSON):
    - `code` (string, required) — the source code or prompt to review.
  - Success response: 200 OK with the model text in the response body (plain text or JSON depending on the service response).
  - Error responses:
    - 400 Bad Request when `code` is missing.
    - 5xx for internal errors (model invocation failures, missing API key, etc.).

Example (PowerShell curl-like using Invoke-RestMethod):

```powershell
Invoke-RestMethod -Method POST -Uri http://localhost:PORT/ai/get-review -ContentType 'application/json' -Body (@{ code = "// your code here" } | ConvertTo-Json)
```

Or with curl (cross-platform):

```bash
curl -X POST http://localhost:PORT/ai/get-review \
  -H "Content-Type: application/json" \
  -d '{"code":"// your code here"}'
```

## How the Gemini model is used

- File: `src/services/ai.service.js`.
- The code uses the official `@google/generative-ai` client and constructs a `GoogleGenerativeAI` instance with an API key read from the environment variable `GEMINI_API_KEY`.
- It requests the `gemini-2.0-flash` model and supplies a `systemInstruction` that frames the model as a senior code reviewer (7+ years experience). That instruction contains guidance on tone, review checklist, and an example of expected output.
- The service exposes `generateContent(prompt)` which calls `model.generateContent(prompt)` and returns `result.response.text()`.

Implementation notes and important details:

- API key: The server expects the Gemini API key in the environment as `GEMINI_API_KEY`. Ensure it is set in your hosting environment or local dev (do not commit keys to source control).
- Model: `gemini-2.0-flash` is used by default. You can change the model name in `ai.service.js` if needed.
- System instruction: The long instruction in `ai.service.js` guides the model to act as a code reviewer. Keep this instruction concise if you hit token limits.
- Response handling: Currently `ai.service.js` returns `result.response.text()`. Depending on the client library version and model, the shape of the response may change — add defensive checks in production.

## Environment & Running

1. Install dependencies (from `BackEnd` folder):

```powershell
cd BackEnd; npm install
```

2. Set environment variable (PowerShell example):

```powershell
$env:GEMINI_API_KEY = "your_gemini_api_key_here"
# Or set it permanently using system environment variables before running the server
```

3. Start the server (project may have a start script in `BackEnd/package.json`):

```powershell
npm start
```

Then send requests to `http://localhost:PORT/ai/get-review` (see `BackEnd/package.json` or `server.js` for the configured port — often 3000).

## Connect with me
- **LinkedIn:** https://www.linkedin.com/in/devadi
- **GitHub:** https://github.com/ADI-2707
