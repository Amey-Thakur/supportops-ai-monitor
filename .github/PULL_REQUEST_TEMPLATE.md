## Summary

<!-- One or two sentences: what does this PR change and why? -->

## Type of change

- [ ] Bug fix (non-breaking change that resolves an issue)
- [ ] New feature (non-breaking addition)
- [ ] Documentation update
- [ ] Test improvement
- [ ] Refactor (no behaviour change)

## Checklist

- [ ] `pytest tests/ -v` passes locally — all 46 tests green
- [ ] `flake8 src/ tests/ --select=E9,F63,F7,F82` — no syntax errors
- [ ] New database functions use `try/finally conn.close()` pattern
- [ ] Simulation mode works without `OPENAI_API_KEY`
- [ ] `CHANGELOG.md` updated under `[Unreleased]` with a brief description

## Related issues

<!-- Closes #ISSUE_NUMBER -->

## Notes for reviewer

<!-- Anything specific the reviewer should look at or test. -->
