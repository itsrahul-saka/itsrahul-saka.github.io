# Backend & Deployment Setup Guide (`SETUP_GUIDE.md`)

This guide explains how to run the **RAS AI** backend proxy locally or deploy it to a free serverless/container host so your **`GROQ_API_KEY`** remains 100% private on the backend while your portfolio frontend runs on **GitHub Pages** (`https://itsrahul-saka.github.io/`).

---

## 1. Why a Backend Proxy Is Required

GitHub Pages is a static file host. Any API key placed inside frontend HTML or JavaScript is publicly visible to anyone who opens Browser DevTools. To keep your key secure:
- The frontend (`index.html`) sends requests to `POST /api/chat` (or your configured proxy URL in **RAS AI → ⚙️ API Settings**).
- The backend proxy (`server/proxy.js`) reads `process.env.GROQ_API_KEY` from server-side environment variables and calls `https://api.groq.com/openai/v1/chat/completions`.

---

## 2. Quick Local Setup (Node.js 18+)

1. Obtain a free API key from [Groq Console (`console.groq.com/keys`)](https://console.groq.com/keys).
2. In the project root directory, copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
3. Open `.env` (which is protected by `.gitignore`) and set your key:
   ```env
   GROQ_API_KEY=gsk_your_actual_groq_key_here
   PORT=8787
   ```
4. Start the proxy server (zero external `npm` packages required — uses built-in Node.js `node:http` and `fetch`):
   ```bash
   node --env-file=.env server/proxy.js
   ```
5. Verify the health endpoint:
   ```bash
   curl http://127.0.0.1:8787/api/health
   ```
   When `GROQ_API_KEY` is set, `/api/health` returns:
   ```json
   {
     "ok": true,
     "connected": true,
     "provider": "groq",
     "models": {
       "Fast": "llama-3.1-8b-instant",
       "Normal": "llama-3.3-70b-versatile",
       "Deep Thinking": "deepseek-r1-distill-llama-70b"
     }
   }
   ```
6. In **RAS AI**, open **⚙️ API Settings**, set the **Backend Proxy Base URL** to `http://127.0.0.1:8787`, and click **🔌 Test Connection**. The status badge will turn green (`🟢 Groq API Connected`).

---

## 3. Production Deployment (GitHub Pages + Free Backend Host)

1. **Frontend (GitHub Pages)**:
   - Commit `index.html`, `404.html`, `private-search.html`, `.gitignore`, `.env.example`, and documentation to [`https://github.com/itsrahul-saka/itsrahul-saka.github.io`](https://github.com/itsrahul-saka/itsrahul-saka.github.io).
   - Confirm via `git status` that `.env` is **not** tracked.
2. **Backend Proxy (Render / Railway / Fly.io Free Tier)**:
   - Deploy `server/proxy.js` with start command `node server/proxy.js`.
   - In the host's Environment Variables dashboard, add:
     - `GROQ_API_KEY` = `<your_groq_api_key>`
     - `ALLOWED_ORIGIN` = `https://itsrahul-saka.github.io`
   - Paste your deployed proxy URL (e.g., `https://ras-ai-proxy.onrender.com`) into **RAS AI → ⚙️ API Settings**.
