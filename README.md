# 🎓 Academic Concierge (SmartCourse Planner)

> An AI-powered study planning agent that turns any syllabus into a real, day-by-day schedule — and stays with you as a conversational study concierge.

Built as a capstone project for the **Kaggle x Google — 5-Day AI Agents: Intensive Vibe Coding Course**.

🔗 **Live demo:** [capstone-project1-three.vercel.app](https://capstone-project1-three.vercel.app/)

---

## 📖 What It Does

Academic Concierge takes the one step most students skip — turning a syllabus into an actual plan — and automates it with an AI agent.

- **Paste a syllabus, get a schedule.** The AI parses raw syllabus text into structured units and topics, then distributes them across a realistic day-by-day timeline.
- **Talk to it like a concierge.** Ask "what's my plan for today?", mark tasks as done, or ask questions about your coursework — all through one conversational interface.
- **Multiple saved conversations.** Like modern AI chat tools, conversations are organized into separate, named chats you can revisit and switch between — not one endless thread.
- **Behavioral analytics.** Beyond simple progress tracking, it surfaces your study streak, flags topics you keep asking about (a sign you're struggling), and gently nudges you if you've gone quiet for a few days.
- **No login required.** Sessions are anonymous and persist locally in your browser — no account creation, no friction.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, FastAPI |
| AI / LLM | OpenRouter (OpenAI-compatible API), free-tier model fallback chain |
| Frontend | Vanilla HTML / CSS / JS (glassmorphic, 3D-inspired UI) |
| Deployment | Vercel (serverless Python functions) |
| Storage | Session-based JSON storage (no external database) |

---

## 🏗️ Architecture

```
├── api/
│   └── index.py          # Vercel serverless entrypoint — imports the FastAPI app
├── app_core.py            # Main FastAPI application (routes, AI logic, session handling)
├── static_content.py      # Base64-embedded frontend assets (served directly by the app)
├── public/                 # Source HTML/CSS/JS (before being embedded into static_content.py)
│   ├── index.html
│   ├── planner.html
│   ├── about.html
│   └── history.html
├── requirements.txt
├── vercel.json
└── .env.example
```

**Why static assets are embedded rather than served from `public/`:** early in deployment, static file serving on Vercel's Python runtime was unreliable in this project's setup. To guarantee the frontend always loads regardless of platform static-hosting behavior, HTML/CSS/JS are base64-encoded directly into `static_content.py` and served by explicit FastAPI routes — removing any dependency on separate CDN-level static routing.

---

## ⚙️ Setup & Local Development

```bash
# Clone the repo
git clone <your-repo-url>
cd academic-concierge

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# then add your OpenRouter API key to .env

# Run locally
uvicorn api.index:app --reload
```

Visit `http://localhost:8000` to view the app locally.

---

## 🔑 Environment Variables

| Variable | Description |
|---|---|
| `OPENROUTER_API_KEY` | Your API key from [openrouter.ai](https://openrouter.ai) — required for AI responses |

Get a free key at OpenRouter (no credit card required) and add it either to your local `.env` file or, for production, your Vercel project's **Settings → Environment Variables**.

---

## ☁️ Deployment (Vercel)

1. Push this repo to GitHub (or deploy directly via the Vercel CLI/dashboard).
2. Import the project in Vercel.
3. Add `OPENROUTER_API_KEY` under **Settings → Environment Variables**.
4. Deploy. Vercel automatically detects `api/index.py` as the Python function entrypoint via `vercel.json`.

---

## 🧠 Key Endpoints

| Endpoint | Description |
|---|---|
| `POST /chat` | Send a message to the AI concierge |
| `POST /upload` | Upload a syllabus file for parsing |
| `GET /conversations/{session_id}` | List all saved conversations for a session |
| `GET /conversations/{session_id}/{conversation_id}` | Get full message history for one conversation |
| `GET /analytics/{session_id}` | Get engagement stats, streaks, and struggle-topic detection |
| `GET /health` | Health check / API key status |

---

## ⚠️ Known Limitations

- **Model consistency:** This project runs on free-tier LLMs via OpenRouter to keep it accessible and cost-free. Free-tier models are noticeably less consistent at following strict formatting instructions than flagship models, so response quality can occasionally vary — this is an active area of improvement rather than a fixed constraint.
- **Session persistence:** Since there's no database or login system, chat history is tied to browser storage and Vercel's serverless session handling, which may reset under certain conditions rather than persisting indefinitely.
- **No user accounts:** By design, for simplicity and privacy — this also means history can't currently be recovered across devices.

---

## 🚀 Future Improvements

- Migrate to a persistent database (e.g. Supabase/Postgres) for reliable long-term chat history
- Improve AI response consistency with stricter output validation and prompt tuning
- Add richer syllabus parsing for more document formats
- Optional user accounts for cross-device history sync

---

## 🎓 Course Context

This project was built during the **Kaggle x Google 5-Day AI Agents: Intensive Vibe Coding Course**, focused on rapid, hands-on AI agent development. It represents 5 days of iterative building, debugging, and deployment — from an initial prototype through multiple rounds of real production fixes.

---

## 📬 Contact

Built by **Krushikar Reddy Yella**.
Feel free to reach out or connect on LinkedIn if you have questions about the project or its architecture.
