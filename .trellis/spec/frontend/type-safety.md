# Type Safety

> Type safety patterns in this project.

---

## Overview

**Not Applicable**: This project is a pure backend AstrBot Plugin with no frontend code.

No TypeScript types are defined because there is no TypeScript code.

---

## Project Type

| Aspect | Status |
|--------|--------|
| TypeScript | ❌ None |
| Python Type Hints | ✅ Used throughout backend |
| Runtime Validation | ✅ Data validation in handlers |

---

## Backend Type Safety

In the backend, we use Python type hints:

### Type Hints Example

```python
# services/models.py
from dataclasses import dataclass, field
from typing import Optional, List

@dataclass
class Article:
    """文章数据模型"""
    id: str
    title: str
    author: str
    content: str
    url: str
    post_time: Optional[str] = None
    feed_images: List[str] = field(default_factory=list)
    view_count: int = 0
    article_type: str = 'unknown'


@dataclass
class SearchResult:
    """搜索结果"""
    keyword: str
    page: int
    items: List[SearchResultItem] = field(default_factory=list)
    total_pages: int = 0
    log_id: Optional[str] = None
    session_id: Optional[str] = None
```

### Function Type Hints

```python
# services/api_client.py
async def fetch_article(url: str) -> Article:
    """根据URL类型获取文章"""

async def fetch_search_results(
    keyword: str,
    page: int = 1,
    log_id: str = None,
    session_id: str = None,
    tag_type: str = None,
    order: str = ''
) -> SearchResult:
    """获取搜索结果"""
```

---

## Related Guidelines

For backend type safety patterns, see [Backend Quality Guidelines](../backend/quality-guidelines.md).
