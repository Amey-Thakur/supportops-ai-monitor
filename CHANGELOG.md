# Changelog

All notable changes to this project are documented here.

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
Versioning: [Semantic Versioning](https://semver.org/spec/v2.0.0.html)

---

## [Unreleased]

### Added
- `src/` directory — Python source files moved from root for cleaner structure
- `assets/screenshots/` directory — visual assets placeholder
- `infrastructure/` directory — deployment guides (renamed from `deploy/`)
- `SECURITY.md` — vulnerability reporting policy
- `CHANGELOG.md` — this file
- `codemeta.json` — machine-readable software metadata (JSON-LD)
- `.github/CONTRIBUTING.md` — contribution guidelines
- `.github/ISSUE_TEMPLATE/bug_report.md` — standardised bug report template
- `.github/ISSUE_TEMPLATE/feature_request.md` — standardised feature request template
- `.github/PULL_REQUEST_TEMPLATE.md` — PR checklist

### Changed
- `deploy/` renamed → `infrastructure/` (git history preserved via `git mv`)
- `Dockerfile` updated for `src/` layout: `PYTHONPATH=/home/user/app/src`, `COPY src/`, `CMD src/app.py`
- `pytest.ini` updated: `pythonpath = src`
- CI workflow: `PYTHONPATH=src` for import check, flake8 scoped to `src/ tests/`

---

## [1.0.0] — 2026-03-01

Initial public release.

### Added
- `ticket_generator.py` — Faker-powered synthetic ticket generation across 5 categories (api, billing, account, safety, other)
- `database.py` — SQLite persistence layer with `tickets` and `api_health_logs` tables
- `ai_triage.py` — OpenAI `gpt-4o-mini` triage with Gaussian simulation fallback (mean ~820ms, 10% error rate)
- `app.py` — Streamlit + Plotly observability dashboard with sidebar controls
- `tests/` — 46-test pytest suite covering all three business logic modules
- `.github/workflows/lint-test.yml` — CI pipeline (flake8 lint + pytest on Ubuntu)
- `Dockerfile` — HuggingFace Spaces Docker SDK deployment (non-root user, healthcheck)
- `docs/` — GitHub Pages terminal-style landing page at `archit-konde.github.io/supportops-ai-monitor/`
- `blog/supportops-ai-monitor.md` — technical writeup covering architecture decisions and lessons learned
- `deploy/huggingface.md` — HuggingFace Spaces deployment guide
- `CITATION.cff` — academic citation metadata

[Unreleased]: https://github.com/Archit-Konde/supportops-ai-monitor/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/Archit-Konde/supportops-ai-monitor/releases/tag/v1.0.0
