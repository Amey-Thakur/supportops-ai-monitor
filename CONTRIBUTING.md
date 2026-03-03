# Contributing to SupportOps AI Monitor

Thanks for your interest. This is a portfolio project, so the contribution bar is intentionally low — most improvements are welcome as long as they fit the project's scope.

---

## What Belongs Here

**Suitable contributions:**
- Bug fixes (simulation accuracy, DB edge cases, Streamlit rendering)
- Documentation improvements (README, blog post corrections, deployment guide)
- New chart types or dashboard panels that fit the existing data model
- Test coverage improvements (currently at 46 tests)

**Out of scope:**
- Replacing SQLite with a different database (intentional architecture choice)
- Breaking changes to the four-module pipeline structure (`ticket_generator → database → ai_triage → app`)
- Adding a build system, bundler, or package manager

If you are unsure whether something fits, open an issue before building it.

---

## How to Contribute

### 1. Fork and clone

```bash
git clone https://github.com/YOUR_USERNAME/supportops-ai-monitor.git
cd supportops-ai-monitor
```

### 2. Set up the environment

```bash
pip install -r "Source Code/requirements.txt"
```

No API key needed — simulation mode is fully functional.

### 3. Run the tests before making changes

```bash
pytest "Source Code/tests/" -v
```

All 46 tests should pass on a clean checkout.

### 4. Make your changes

Follow the existing code style:
- Line length max: 120 characters (matches flake8 config in CI)
- No new dependencies unless clearly justified
- Any new database function follows the `try/finally conn.close()` pattern in `src/database.py`

### 5. Run CI checks locally

```bash
# Lint — syntax errors (must be clean)
flake8 "Source Code/src/" "Source Code/tests/" --count --select=E9,F63,F7,F82 --show-source --statistics

# Style warnings (non-blocking)
flake8 "Source Code/src/" "Source Code/tests/" --count --exit-zero --max-line-length=120 --statistics

# Tests
pytest "Source Code/tests/" -v --tb=short
```

### 6. Open a pull request

Use the PR template. Keep the description focused on what changed and why.

---

## Code of Conduct

Be direct, be constructive, assume good intent.
