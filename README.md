# Multi-Modal AI Content Marketing Engine
## Member 2 — Backend Architecture & Task Queue Operations

---

## Project Overview
A production-grade async backend API that powers the Multi-Modal AI Content
Marketing Engine. Accepts campaign briefs and processes them through a
distributed task queue to generate AI-powered marketing content including
blog posts, tweets, SEO metadata, and promotional images.

---

## My Responsibilities (Member 2)
- REST API setup using FastAPI
- Redis + Celery async task queue
- POST /generate and GET /tasks/{id} endpoints
- Anthropic Claude AI integration with fallback
- Unsplash image generation integration
- Parallel execution (50% latency reduction)
- Schema validation (100% adherence)
- Error handling and logging
- API testing with pytest

---

## Tech Stack
| Technology | Purpose |
|------------|---------|
| Python 3.13 | Core language |
| FastAPI | REST API framework |
| Celery 5.3.4 | Async task queue |
| Redis | Message broker |
| Anthropic Claude | AI text generation |
| Unsplash API | Image fetching |
| Pydantic | Schema validation |
| Pytest | API testing |
| Uvicorn | ASGI server |

---

## Project Structure
multimodal-ai-content-engine/
├── backend/
│   ├── main.py
│   ├── celery_worker.py
│   ├── tasks.py
│   ├── schemas.py
│   ├── routes/
│   │   └── campaign.py
│   ├── services/
│   │   ├── ai_service.py
│   │   ├── image_service.py
│   │   └── validator_service.py
│   └── tests/
│       └── test_api.py
├── requirements.txt
├── .gitignore
└── README.md

---

## API Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | / | Root health check |
| GET | /health | Service health status |
| POST | /generate | Submit campaign brief |
| GET | /tasks/{task_id} | Check task status + results |

---

## Sample Request
POST /generate
{
  "campaign_brief": "eco-friendly sneakers",
  "tone": "casual",
  "target_audience": "young adults"
}

## Sample Response
GET /tasks/{task_id}
{
  "task_id": "abc-123",
  "status": "completed",
  "result": {
    "blog_post": {
      "title": "Introducing eco-friendly sneakers",
      "content_markdown": "..."
    },
    "social_media": {
      "twitter_variants": ["tweet1", "tweet2", "tweet3"]
    },
    "seo_metadata": {
      "meta_title": "Best eco-friendly sneakers",
      "meta_description": "...",
      "keywords": ["eco-friendly", "sneakers"]
    },
    "images": [
      {
        "url": "https://images.unsplash.com/...",
        "alt_description": "sneakers photo",
        "photographer": "John Doe"
      }
    ],
    "_meta": {
      "execution_time_seconds": 1.27,
      "mode": "parallel",
      "schema_validated": true
    }
  }
}

---

## PRD KPIs Achieved
| KPI | Target | Status |
|-----|--------|--------|
| Zero Client Timeouts | Long tasks run in background | ✅ Celery async queue |
| 50% Latency Reduction | Parallel execution | ✅ ThreadPoolExecutor |
| Schema Adherence | 100% clean JSON | ✅ Pydantic validators |
| API Tests | All passing | ✅ 6/6 tests passed |

---

## How to Run Locally

1. Clone the repo
git clone https://github.com/Harsha30012005/Multimodal-AI-content-engine.git
cd Multimodal-AI-content-engine

2. Create virtual environment
python -m venv venv
venv\Scripts\activate

3. Install dependencies
pip install -r requirements.txt

4. Setup .env file in backend folder
REDIS_URL=redis://localhost:6379/0
CELERY_BROKER_URL=redis://localhost:6379/0
CELERY_RESULT_BACKEND=redis://localhost:6379/0
ANTHROPIC_API_KEY=your-key-here
UNSPLASH_ACCESS_KEY=your-key-here

5. Make sure Redis is running as Windows service

6. Start Celery Worker in Terminal 1
cd backend
celery -A celery_worker worker --loglevel=info -P solo

7. Start FastAPI in Terminal 2
cd backend
uvicorn main:app --reload

8. Run Tests
cd backend
pytest tests/test_api.py -v

9. Visit Swagger UI
http://127.0.0.1:8000/docs

---

## Week Summary
| Week | Focus | Status |
|------|-------|--------|
| Week 1 | Backend foundation, Redis, Celery, API endpoints | ✅ Complete |
| Week 2 | AI integration, parallel execution, schema validation, testing | ✅ Complete |
| Week 3 | Docker, optimization, production ready | 🔜 In Progress |