# State Management

> How state is managed in this project.

---

## Overview

**Not Applicable**: This project is a pure backend AstrBot Plugin with no frontend code.

No frontend state management (Redux, Zustand, etc.) is used.

---

## Project Type

| Aspect | Status |
|--------|--------|
| Global State | ❌ None |
| Local State | ❌ None |
| Server State | ✅ Backend handles data |

---

## Backend Equivalent

In the backend, state is managed through:

| Frontend Concept | Backend Equivalent |
|------------------|-------------------|
| Global store | Service class instance |
| Local state | Instance variables |
| Server state | API client + cache |
| Persistence | JSON file storage |

### Example: Session State

```python
# services/session_manager.py
@dataclass
class SearchSession:
    """搜索会话状态 - 替代前端的全局状态"""
    keyword: str
    tag_type: Optional[str] = None
    order: str = ''
    current_page: int = 1
    total_pages: int = 1
    log_id: Optional[str] = None
    session_id: Optional[str] = None


class SessionManager:
    """会话管理器 - 持久化到 JSON 文件"""
    def __init__(self, data_path: Path):
        self.sessions_file = data_path / "sessions.json"

    def get(self, user_id: str) -> Optional[SearchSession]:
        # Load from persistence

    def set(self, user_id: str, session: SearchSession):
        # Save to persistence
```

---

## Related Guidelines

For backend data persistence, see [Backend Database Guidelines](../backend/database-guidelines.md).
