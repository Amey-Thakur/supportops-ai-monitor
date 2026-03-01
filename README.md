# SupportOps AI Monitor 🎫

A Python-based support operations dashboard that simulates and monitors enterprise AI platform support workflows. Built to demonstrate real-world technical support skills including log analysis, API health monitoring, ticket triage, SQL querying, JSON parsing, and observability dashboarding.

> **Built as a portfolio project to demonstrate skills for Enterprise AI Support / Technical Support Engineer roles.**

---

## What It Does

- **Generates realistic support tickets** — simulates the kind of tickets an OpenAI/AI platform support team receives: API errors, billing disputes, account issues, safety concerns
- **AI-powered ticket triage** — calls the OpenAI API to categorize tickets by type, analyze customer sentiment, and generate one-line summaries
- **API health monitoring** — logs every API call with latency, HTTP status code, and error type (mirrors Datadog/Splunk-style observability)
- **Operational dashboard** — visualizes ticket volume, priority distribution, category breakdown, sentiment trends, API error rates, and latency over time
- **SQLite persistence** — all data stored in a local database with queryable tables

---

## Technical Skills Demonstrated

| Skill | How It's Used |
|-------|---------------|
| **JSON parsing** | Ticket data ingestion, OpenAI API request/response handling |
| **SQL (SQLite)** | Ticket storage, aggregate stats queries, filtering |
| **API troubleshooting** | OpenAI API calls with error handling (429, 500, 408), structured logging |
| **Log analysis** | `api_health_logs` table mirrors real observability — latency, error types, status codes |
| **Dashboard/monitoring** | Streamlit + Plotly charts for real-time operational visibility |
| **Python** | Core application logic, data pipeline, CLI tooling |
| **Git/GitHub** | Version controlled, documented, open source |

---

## Tech Stack

- **Python 3.11+**
- **Streamlit** — dashboard framework
- **SQLite** — persistent storage
- **OpenAI API** (`gpt-4o-mini`) — ticket triage
- **Plotly** — interactive charts
- **Pandas** — data manipulation
- **Faker** — realistic test data generation

---

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/Archit-Konde/supportops-ai-monitor.git
cd supportops-ai-monitor
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Set up environment variables
```bash
cp .env.example .env
# Edit .env and add your OpenAI API key (optional — app works without it using simulation mode)
```

### 4. Run the dashboard
```bash
streamlit run app.py
```

The app opens at `http://localhost:8501`. Use the sidebar to generate tickets and run AI triage.

---

## Without an OpenAI API Key

The app runs in **simulation mode** when no API key is provided. The simulation realistically models:
- API latency (Gaussian distribution, mean ~820ms)
- 10% error rate with realistic error type distribution (rate limits, server errors, timeouts)
- HTTP status codes (200, 429, 500, 408)

This means the full dashboard is demonstrable without any API costs.

---

## Project Structure

```
supportops-ai-monitor/
├── app.py                  # Streamlit dashboard (main entry point)
├── database.py             # SQLite schema, queries, and connection management
├── ticket_generator.py     # Realistic support ticket generation
├── ai_triage.py            # OpenAI API calls + health logging
├── requirements.txt
├── .env.example
├── data/                   # JSON ticket exports
├── logs/                   # Application logs
└── db/                     # SQLite database file
```

---

## Database Schema

### `tickets`
| Column | Type | Description |
|--------|------|-------------|
| `ticket_id` | TEXT | Unique ticket identifier (TKT-XXXXXXXX) |
| `created_at` | TEXT | ISO timestamp |
| `customer` | TEXT | Company name |
| `subject` | TEXT | Ticket subject |
| `body` | TEXT | Full ticket description |
| `priority` | TEXT | low / medium / high / critical |
| `status` | TEXT | open / in_progress / resolved |
| `category` | TEXT | AI-assigned: api / billing / account / safety / other |
| `sentiment` | TEXT | AI-assigned: positive / neutral / negative |
| `ai_summary` | TEXT | AI-generated one-line summary |
| `resolved_at` | TEXT | Resolution timestamp |

### `api_health_logs`
| Column | Type | Description |
|--------|------|-------------|
| `timestamp` | TEXT | ISO timestamp of API call |
| `endpoint` | TEXT | API endpoint called |
| `status_code` | INTEGER | HTTP response code |
| `latency_ms` | REAL | Response time in milliseconds |
| `success` | INTEGER | 1 = success, 0 = failure |
| `error_type` | TEXT | rate_limit / server_error / timeout / null |
| `ticket_id` | TEXT | Associated ticket |

---

## Key SQL Queries

```sql
-- Ticket volume by category
SELECT category, COUNT(*) as count
FROM tickets
WHERE category IS NOT NULL
GROUP BY category ORDER BY count DESC;

-- API error rate
SELECT
  COUNT(*) as total_calls,
  SUM(CASE WHEN success = 0 THEN 1 ELSE 0 END) as failures,
  ROUND(AVG(CASE WHEN success = 0 THEN 1.0 ELSE 0 END) * 100, 1) as error_rate_pct
FROM api_health_logs;

-- P95 API latency
SELECT latency_ms
FROM api_health_logs
WHERE success = 1
ORDER BY latency_ms
LIMIT 1 OFFSET (SELECT CAST(COUNT(*) * 0.95 AS INT) FROM api_health_logs WHERE success = 1);

-- High priority open tickets
SELECT ticket_id, customer, subject, priority, created_at
FROM tickets
WHERE status = 'open' AND priority IN ('critical', 'high')
ORDER BY created_at ASC;
```

---

## Author

**Archit Konde** — Machine Learning Engineer  
[archit-konde.github.io](https://archit-konde.github.io) · [GitHub](https://github.com/Archit-Konde) · [LinkedIn](https://linkedin.com/in/architkonde)
