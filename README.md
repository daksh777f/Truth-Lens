# 🔍 TrustLens — AI Trust & Context Layer for Web Content

<div align="center">

![TrustLens](https://img.shields.io/badge/TrustLens-AI%20Trust%20Layer-00875A?style=for-the-badge&logo=shield&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-18+-61DAFB?style=flat-square&logo=react&logoColor=black)
![LangGraph](https://img.shields.io/badge/LangGraph-Multi--Agent-FF6B6B?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

**Transform how people evaluate online information with transparent, evidence-based verification.**

[Demo](#-quick-start) • [API Docs](#-api-usage) • [Architecture](#-architecture) • [Extension](#-browser-extension)

</div>

---

## 🎯 What is TrustLens?

TrustLens is an AI-powered multi-agent system that adds a transparent "trust overlay" to any webpage. Instead of blindly trusting online content or spending hours manually fact-checking, TrustLens:

- **Extracts factual claims** from any webpage or text
- **Retrieves evidence** from authoritative sources across the web
- **Rates each claim** with confidence scores and reasoning
- **Highlights claims** with intuitive color-coding
- **Shows you the evidence** so YOU decide what to believe

### 🎨 Visual Verdict System

| Color          | Verdict            | Meaning                                |
| -------------- | ------------------ | -------------------------------------- |
| 🟢 Dark Green  | Strongly Supported | Multiple authoritative sources confirm |
| 🟢 Light Green | Supported          | Evidence generally supports the claim  |
| 🟡 Yellow      | Mixed/Uncertain    | Conflicting evidence or outdated       |
| 🟠 Orange      | Weak               | Limited or unreliable support          |
| 🔴 Red         | Contradicted       | Evidence contradicts the claim         |
| ⚪ Gray        | Not Verifiable     | Opinion or cannot be fact-checked      |

### 🚫 What We're NOT

- **NOT a content moderator** — We don't block or censor anything
- **NOT a political truth arbiter** — We focus on objective, verifiable claims
- **NOT overconfident** — We show uncertainty clearly and always link to sources

## 🎪 Focus Verticals (MVP)

1. **E-commerce & SaaS** — Product claims, warranties, customer counts
2. **Learning & Technical Content** — Blog posts, tutorials, educational content
3. **Professional Content** — LinkedIn posts, reports, whitepapers

---

## 🏗️ Architecture

### Multi-Agent System (LangGraph)

```
┌─────────────────┐
│  Ingestion      │ ─── URL/HTML/Text cleanup
└────────┬────────┘
         ▼
┌─────────────────┐
│ Claim Decomposer│ ─── Extract factual claims
└────────┬────────┘
         ▼
┌─────────────────┐
│ Claim Classifier│ ─── Filter opinions, tag topics
└────────┬────────┘
         ▼
┌─────────────────┐
│  Query Planner  │ ─── Plan search strategies
└────────┬────────┘
         ▼
┌─────────────────────────────────────┐
│  Retrieval Workers (Parallel)       │
│  ┌────────┐ ┌────────┐ ┌─────────┐  │
│  │ Web    │ │Wikipedia│ │ Domain  │  │
│  │ Search │ │  API   │ │Specific │  │
│  └────────┘ └────────┘ └─────────┘  │
└────────────────┬────────────────────┘
                 ▼
┌─────────────────┐
│ Evidence Ranker │ ─── Score & rank by relevance
└────────┬────────┘
         ▼
┌─────────────────────────────────────┐
│  Verification (Optional Multi-Model)│
│  ┌─────────┐        ┌─────────┐     │
│  │ GPT-4o  │   ⟷   │ Claude  │     │
│  └─────────┘        └─────────┘     │
└────────────────┬────────────────────┘
                 ▼
┌─────────────────┐
│Cross-Verification│ ─── Reconcile model disagreements
└────────┬────────┘
         ▼
┌─────────────────┐
│ Explanation/UX  │ ─── Generate user-friendly output
└────────┬────────┘
         ▼
┌─────────────────────────────────────┐
│  Optional: Blockchain Anchoring     │
│  (Tamper-proof verification receipt)│
└─────────────────────────────────────┘
```

### Tech Stack

| Layer         | Technology                                 |
| ------------- | ------------------------------------------ |
| **Backend**   | Python 3.10+, FastAPI, LangGraph           |
| **Frontend**  | Next.js 14, React 18, TypeScript, Tailwind |
| **Extension** | Chrome Manifest V3                         |
| **Database**  | SQLite (dev), PostgreSQL (prod)            |
| **LLMs**      | Groq (Llama 3.3 70B - FREE)                |
| **Search**    | DuckDuckGo (FREE), optional: SerpAPI       |

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Node.js 18+
- Groq API Key (free at [console.groq.com](https://console.groq.com))

### 1️⃣ Get Your Free Groq API Key

1. Go to [console.groq.com](https://console.groq.com)
2. Sign up (free)
3. Create an API key
4. Copy the key

### 2️⃣ Backend Setup

```powershell
cd backend

# Edit the .env file and add your GROQ_API_KEY
notepad .env

# Install dependencies
pip install -r requirements.txt

# Set Python path and run server
$env:PYTHONPATH = (Get-Location).Path
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

The backend uses **SQLite** by default (no database setup needed!) and **DuckDuckGo** for free web search.

### 3️⃣ Frontend Setup (Optional)

```powershell
cd frontend
npm install
npm run dev
```

### 4️⃣ Chrome Extension

1. Open Chrome and go to `chrome://extensions/`
2. Enable "Developer mode" (top right)
3. Click "Load unpacked"
4. Select the `extension` folder

### Access Points

- 🌐 **Web App**: http://localhost:3000
- 📚 **API Docs**: http://127.0.0.1:8000/docs
- 🔧 **API Base**: http://127.0.0.1:8000/api/v1
- ❤️ **Health**: http://127.0.0.1:8000/health

### 🆓 Free APIs Used

| Service        | Purpose             | Free Tier        |
| -------------- | ------------------- | ---------------- |
| **Groq**       | LLM (Llama 3.3 70B) | 14,400 req/day   |
| **DuckDuckGo** | Web Search          | Unlimited        |
| **SQLite**     | Database            | Local, unlimited |

---

## 📚 API Usage

### Verify Content

```bash
curl -X POST http://localhost:8000/v1/verify \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "text": "Our product is used by over 10,000 teams worldwide and reduces costs by 50%.",
    "url": "https://example.com/product",
    "vertical": "saas"
  }'
```

### Response

```json
{
  "verification_id": "ver_abc123def456",
  "page_score": 72,
  "summary": {
    "strongly_supported": 1,
    "supported": 1,
    "mixed": 0,
    "weak": 1,
    "contradicted": 0
  },
  "claims": [
    {
      "id": "clm_001",
      "span": [0, 51],
      "text": "Our product is used by over 10,000 teams worldwide",
      "verdict": "supported",
      "confidence": 0.82,
      "reasoning": "Multiple sources confirm usage figures around 10,000-12,000 teams as of 2024.",
      "sources": {
        "supporting": [
          {
            "url": "https://company.com/about",
            "snippet": "Trusted by 12,000+ teams globally",
            "domain_score": 0.85,
            "published_at": "2024-08-15"
          }
        ],
        "contradicting": []
      }
    },
    {
      "id": "clm_002",
      "span": [56, 78],
      "text": "reduces costs by 50%",
      "verdict": "weak",
      "confidence": 0.35,
      "reasoning": "No independent verification found. Only company marketing materials make this claim.",
      "sources": {
        "supporting": [],
        "contradicting": []
      }
    }
  ],
  "metadata": {
    "processing_time_ms": 8420,
    "models_used": ["gpt-4o"],
    "sources_checked": 24
  }
}
```

### Get Verification Status

```bash
curl http://localhost:8000/v1/verification/ver_abc123def456
```

---

## 🌐 Browser Extension

### Installation

1. Build the extension:

```bash
cd extension
npm install
npm run build
```

2. Load in Chrome:
   - Navigate to `chrome://extensions/`
   - Enable "Developer mode"
   - Click "Load unpacked"
   - Select `extension/dist` folder

### Usage

1. Navigate to any webpage
2. Click the TrustLens icon in your toolbar
3. Wait for analysis (15-30 seconds)
4. View highlighted claims with color coding
5. Hover for quick tooltips, click for detailed evidence

---

## 📁 Project Structure

```
trustlens/
├── backend/                 # Python FastAPI backend
│   ├── app/
│   │   ├── agents/         # LangGraph agent definitions
│   │   ├── api/            # API routes
│   │   ├── core/           # Config, security, database
│   │   ├── models/         # SQLAlchemy models
│   │   ├── schemas/        # Pydantic schemas
│   │   └── services/       # Business logic
│   ├── tests/
│   └── alembic/            # Database migrations
├── frontend/               # React web application
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── pages/          # Page components
│   │   ├── hooks/          # Custom hooks
│   │   └── lib/            # Utilities
│   └── public/
├── extension/              # Chrome browser extension
│   ├── src/
│   │   ├── popup/          # Extension popup
│   │   ├── content/        # Content scripts
│   │   └── background/     # Service worker
│   └── public/
├── contracts/              # Solidity smart contracts (optional)
└── docs/                   # Documentation
```

---

## 🗺️ Roadmap

### ✅ Phase 0 — MVP (Hackathon Ready)

- [x] Web app with text input
- [x] Core agent pipeline
- [x] Claim extraction & verification
- [x] Color-coded highlighting
- [x] Page scoring

### 🔄 Phase 1 — Extension & Multi-Agent

- [ ] Browser extension for Chrome/Edge
- [ ] Parallel retrieval workers
- [ ] Cross-model verification
- [ ] Real-time agent visualization

### 📋 Phase 2 — API & Reputation

- [ ] Public REST API with rate limiting
- [ ] Domain reputation tracking
- [ ] Organization dashboard
- [ ] Historical accuracy trends

### 🔮 Phase 3 — Advanced Features

- [ ] Blockchain anchoring (Polygon)
- [ ] Time-decay re-verification
- [ ] Multilingual support
- [ ] Custom knowledge bases

---

## 🤔 FAQ

**Q: Are you deciding what's true on the internet?**

> No. We don't block or hide content; we surface evidence and model confidence. We're a decision support tool, not a censorship engine.

**Q: What about political bias?**

> Our MVP focuses on practical verticals: commerce, education, professional content. Political content is explicitly out of scope to avoid bias.

**Q: What if the model hallucinates?**

> We mitigate this by: (1) Always tying verdicts to explicit external sources, (2) Cross-verifying with multiple models, (3) Showing uncertainty clearly.

**Q: Why blockchain?**

> Optional feature for tamper-proof receipts. If content changes later, you can detect it. SaaS-only works fine; blockchain is an extra layer.

---

## Team

- Daksh Goel ([@daksh777f](https://github.com/daksh777f))
- Alcasinator
- SahilShah288
- Pulkit Saraf

<!-- TODO (Daksh): after each name, add one line on what that person built, e.g. "backend API and data pipeline". Hidden comments like this one do not show on GitHub. -->

## 📄 License

MIT License - See [LICENSE](LICENSE) file

---

## 🤝 Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

---

<div align="center">

**Built with ❤️ for a more transparent web**

[⬆ Back to Top](#-trustlens--ai-trust--context-layer-for-web-content)

</div>
