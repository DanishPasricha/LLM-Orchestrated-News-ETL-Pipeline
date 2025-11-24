# 🌐 AI News Intelligence Pipeline

**LLM-Powered Automated AI News Aggregator, Summarizer & Email Digest System**

This project is an **end-to-end autonomous AI news monitoring pipeline** that collects the latest updates from major AI sources (YouTube AI channels, OpenAI, Anthropic), enriches the content using transcripts & markdown extraction, generates concise digests using LLMs, ranks them based on a customizable user profile, and finally emails a clean, curated daily digest.

The system runs like a mini autonomous agent workflow with **ETL → Enrichment → LLM Digests → Ranking → Email Delivery**.

Perfect for personal research monitoring, newsletters, or daily AI insights.

---

## 🚀 Features

* **Automated scraping**

  * YouTube AI channels
  * OpenAI News (RSS)
  * Anthropic Blog (RSS)

* **Content enrichment**

  * YouTube transcript extraction
  * Anthropic article → Markdown conversion

* **Digest generation (LLMs)**

  * GPT-4o-mini creates structured summaries
  * Domain-aware summaries based on article type

* **AI ranking agent**

  * Personalizes digest ordering based on user interests
  * Uses relevance scoring + reasoning

* **Automatic email digest**

  * Generates Markdown & HTML email
  * Sends curated list via SMTP

* **Full persistence**

  * PostgreSQL + SQLAlchemy ORM
  * Stores raw articles, transcripts, markdown, digests

---

# 🧠 Tech Stack

| Layer                  | Technology                           |
| ---------------------- | ------------------------------------ |
| **Language**           | Python 3.11                          |
| **Scraping**           | feedparser, youtube-transcript-api   |
| **Content Extraction** | Docling (HTML → Markdown conversion) |
| **LLM Agents**         | OpenAI Responses API (GPT-4o-mini)   |
| **Database**           | PostgreSQL, SQLAlchemy ORM           |
| **Email Delivery**     | SMTP + MIME (HTML + Markdown)        |
| **Environment**        | python-dotenv                        |
| **Deployment**         | Docker Compose (Postgres container)  |

---

# 🔄 High-Level Workflow Diagram (Colored)

The diagram below is fully GitHub-friendly and uses ANSI-style colors.

```
               ┌──────────────────────────────────────────────────┐
               │                🌐 Data Sources                   │
               │                                                  │
               │  🟥 YouTube AI Channels                          │
               │  🟦 OpenAI News RSS                              │
               │  🟩 Anthropic Blog RSS                           │
               └──────────────────────────────────────────────────┘
                                  │
                                  ▼
                    ┌──────────────────────────┐
                    │   🟧 Scraping Layer      │
                    │ - Fetch RSS feeds        │
                    │ - Fetch YouTube videos   │
                    └──────────────────────────┘
                                  │
                                  ▼
               ┌──────────────────────────────────────────────────┐
               │               🟪 Enrichment Layer                 │
               │ - YouTube → Transcript extraction                │
               │ - Anthropic → HTML → Markdown conversion         │
               └──────────────────────────────────────────────────┘
                                  │
                                  ▼
                     ┌──────────────────────────┐
                     │   🟨 Database Layer       │
                     │ PostgreSQL + SQLAlchemy  │
                     │ - Store raw articles     │
                     │ - Store transcripts      │
                     │ - Store markdown         │
                     └──────────────────────────┘
                                  │
                                  ▼
         ┌──────────────────────────────────────────────────────────┐
         │                  🟦 LLM Digest Agent                      │
         │  GPT-4o-mini: Summaries for each article/video           │
         │  Output → Title + Summary (structured)                   │
         └──────────────────────────────────────────────────────────┘
                                  │
                                  ▼
         ┌──────────────────────────────────────────────────────────┐
         │                  🟩 Ranking Agent                         │
         │ - Understands user profile                               │
         │ - Assigns relevance scores                               │
         │ - Orders articles for digest                             │
         └──────────────────────────────────────────────────────────┘
                                  │
                                  ▼
             ┌─────────────────────────────────────────────┐
             │            🟨 Email Digest Builder           │
             │ - Markdown + HTML generation                │
             │ - Curated list of top N items               │
             └─────────────────────────────────────────────┘
                                  │
                                  ▼
                     ┌──────────────────────────┐
                     │      🟦 SMTP Email        │
                     │   Daily AI Digest Email  │
                     └──────────────────────────┘
```

---

# 📦 Project Structure

```
ai-news-intelligence-pipeline/
│
├── app/
│   ├── agent/           # Digest agent, ranking agent, email agent
│   ├── scrapers/        # YouTube, OpenAI, Anthropic scrapers
│   ├── services/        # Transcript processing, markdown extraction, email
│   ├── database/        # SQLAlchemy models & repository
│   ├── config.py        # Channel list + settings
│   └── daily_runner.py  # Full pipeline orchestration
│
├── docker/
│   └── docker-compose.yml  # Postgres container
│
├── main.py                # CLI entrypoint
├── pyproject.toml         # Dependencies
└── example.env            # Environment variables
```

---

# ⚙️ How It Works (Short Summary)

1. **Scrapers** pull new videos & articles from YouTube, OpenAI, Anthropic.
2. **Processing layer** enriches them with transcripts or markdown.
3. **Digest Agent (LLM)** summarizes each piece into short, high-value digests.
4. **Curator Agent (LLM)** ranks articles based on a personalized user profile.
5. **Email Agent** generates a clean digest in HTML & Markdown.
6. **SMTP Service** sends a daily email to the user.

---

# 📥 Setup (Quick Start)

```bash
cp example.env .env
docker compose up -d  # Start PostgreSQL
pip install -r requirements.txt (or poetry install)
python app/database/create_tables.py
python main.py 24 10
```


Just tell me — I can refine this to make your repo look premium.
