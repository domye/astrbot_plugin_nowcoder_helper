# Hook Guidelines

> How hooks are used in this project.

---

## Overview

**Not Applicable**: This project is a pure backend AstrBot Plugin with no frontend code.

No React hooks are used because there is no React application.

---

## Project Type

| Aspect | Status |
|--------|--------|
| React Hooks | ❌ None |
| Custom Hooks | ❌ None |
| Data Fetching | ✅ Backend (aiohttp) |

---

## Backend Equivalent

In the backend, "stateful logic" is handled through:

| Frontend Concept | Backend Equivalent |
|------------------|-------------------|
| useState | Instance variables in classes |
| useEffect | Lifecycle methods (initialize/terminate) |
| useContext | Context object from AstrBot |
| Custom hooks | Service classes |

### Example: Session Management

Instead of a React hook, we use a service class:

```python
# services/session_manager.py
class SessionManager:
    """会话管理器 - 替代前端的 useState/useContext"""
    def __init__(self, data_path: Path):
        self.sessions_file = data_path / "sessions.json"

    def get(self, user_id: str) -> Optional[SearchSession]:
        return SearchSession(**data[user_id]) if user_id in data else None

    def set(self, user_id: str, session: SearchSession):
        data[user_id] = asdict(session)
        self._save(data)
```

---

## Related Guidelines

For backend patterns, see [Backend Event Handling](../backend/event-handling.md).
