# Quality Guidelines

> Code quality standards for frontend development.

---

## Overview

**Not Applicable**: This project is a pure backend AstrBot Plugin with no frontend code.

No frontend quality guidelines are defined.

---

## Project Type

| Aspect | Status |
|--------|--------|
| Frontend Linting | ❌ None |
| Frontend Testing | ❌ None |
| Backend Linting | ✅ Python (ruff/flake8) |
| Backend Testing | ✅ pytest |

---

## Backend Quality Standards

For backend quality guidelines, see:

- [Backend Quality Guidelines](../backend/quality-guidelines.md) - Code standards, async patterns
- [Backend Error Handling](../backend/error-handling.md) - Exception patterns
- [Backend Logging Guidelines](../backend/logging-guidelines.md) - AstrBot logger usage

---

## Backend Quality Checklist

From the backend guidelines:

- [ ] All handlers have docstrings
- [ ] All handlers use async/await
- [ ] All handlers use yield (not return)
- [ ] Type hints on all functions
- [ ] Error handling in all handlers
- [ ] No global variables
- [ ] No blocking operations in async
- [ ] Files under size limits
- [ ] Linting passes (ruff/flake8)
