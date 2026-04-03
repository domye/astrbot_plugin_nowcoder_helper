# 牛客文章助手 - AstrBot 插件

> **智能获取牛客网文章的 AstrBot 插件**

支持文章解析、关键词搜索、智能筛选、交互式多轮对话。

> [!NOTE]
> 这是一个 [AstrBot](https://github.com/AstrBotDevs/AstrBot) 插件。
>
> [AstrBot](https://github.com/AstrBotDevs/AstrBot) 是一个支持多平台的智能对话机器人框架。

---

## 功能特性

- 🔗 **智能链接识别**: 自动识别牛客网文章链接
- 🔍 **关键词搜索**: 支持搜索文章并筛选类型
- 📄 **文章解析**: 获取完整文章内容（支持 Markdown 格式）
- 📑 **交互式多轮对话**: 搜索后可选翻页、查看详情
- 👤 **用户会话隔离**: 群聊中每个用户的会话独立
- ⏱️ **会话超时**: 1分钟无操作自动退出
- 💾 **会话持久化**: AstrBot 重启后恢复未完成的会话
- 🏷️ **智能筛选**: 支持按类型筛选（面经、题解、讨论等）
- 📊 **排序方式**: 支持按相关度或最新排序

---

## 安装

### 依赖安装

```bash
pip install aiohttp beautifulsoup4 lxml
```

### 插件安装

将本插件目录放入 AstrBot 的 `addons/plugins/` 目录下即可。

---

## 使用方法

### 基本用法

发送以 `牛客` 开头的消息即可触发：

```
牛客 <关键词> [筛选类型] [排序方式]
```

### 命令示例

| 输入 | 功能 |
|------|------|
| `牛客 面经` | 搜索"面经"相关文章 |
| `牛客 面经 最新` | 搜索并按最新排序 |
| `牛客 https://www.nowcoder.com/discuss/12345` | 解析指定文章链接 |

### 支持的筛选类型

| 类型 | 说明 |
|------|------|
| 面经 | 面试经验分享 |
| 题解 | 算法题解 |
| 讨论 | 技术讨论 |
| 知识 | 知识点总结 |
| 公司 | 公司相关 |
| 其他 | 其他类型 |

### 交互流程示例

**场景1: 搜索文章**

```
用户: 牛客 阿里巴巴面经
Bot: 正在搜索: 阿里巴巴面经...

     搜索结果: 阿里巴巴面经
     第 1 页 / 共 5 页

     1. 阿里巴巴Java开发岗位面经分享
     2. 腾讯校招面试经验总结
     3. 字节跳动后端开发面试题
     4. 阿里巴巴前端面经2024
     5. 阿里Java实习面试经验

     输入编号查看文章，或：
     - 发送 '下一页' 查看更多
     - 发送 '退出' 取消

用户: 下一页
Bot: [显示第2页结果]

用户: 1
Bot: 正在获取文章...

     [返回完整文章内容，Markdown格式]

     输入编号查看其他文章，或发送'退出'

用户: 退出
Bot: 已退出
```

**场景2: 直接解析链接**

```
用户: 牛客 https://www.nowcoder.com/discuss/123456
Bot: 正在获取文章...

     [返回文章完整内容]
```

**场景3: 筛选和排序**

```
用户: 牛客 动态规划 题解 最新
Bot: 正在搜索: 动态规划 | 筛选: 题解 | 排序: 最新...
```

---

## 会话控制

在交互过程中，你可以：

| 输入 | 功能 |
|------|------|
| `1-10` | 选择对应编号的文章 |
| `下一页` / `next` | 查看下一页结果 |
| `上一页` / `prev` | 查看上一页结果 |
| `返回` / `back` | 返回搜索结果列表 |
| `退出` / `quit` | 结束当前会话 |

### 会话特性

- **超时**: 60秒无操作自动退出
- **隔离**: 每个用户会话独立，互不影响
- **持久化**: 重启 AstrBot 后可恢复会话

---

## 支持的文章类型

| 类型 | URL 格式 |
|------|----------|
| Discuss | `https://www.nowcoder.com/discuss/{id}` |
| Feed | `https://www.nowcoder.com/feed/main/detail/{id}` |

---

## 技术架构

```
nowcoder_helper/
├── main.py                    # 插件入口
├── metadata.yaml              # 插件元数据
├── handlers/                  # 命令处理器
│   ├── __init__.py
│   ├── search_handler.py      # 搜索 + 多轮对话
│   └── article_handler.py     # 文章链接处理
├── services/                  # 业务逻辑
│   ├── __init__.py
│   ├── api_client.py          # 异步 HTTP 请求
│   ├── parser.py              # HTML/JSON 解析
│   ├── formatter.py           # 消息格式化
│   ├── models.py              # 数据模型
│   ├── session_manager.py     # 会话管理
│   └── constants.py           # 常量配置
└── README.md
```

### 核心技术

- `session_waiter` - 多轮对话会话控制
- `SessionController` - 会话生命周期管理
- `aiohttp` - 异步 HTTP 请求
- `BeautifulSoup` - HTML 解析
- `get_astrbot_data_path()` - 会话状态持久化

---

## 注意事项

1. **会话超时**: 搜索会话60秒无操作自动退出
2. **搜索结果**: 默认每页10条结果
3. **文章长度**: 长文章会自动分段发送
4. **网络依赖**: 需要能访问牛客网
5. **数据存储**: 会话数据保存在 `data/plugin_data/nowcoder_helper/` 目录

---

## 更新日志

### v1.0.0
- 智能链接识别
- 关键词搜索
- 多轮对话交互
- 文章类型筛选
- 排序方式支持

---

## 相关链接

- [AstrBot 官方仓库](https://github.com/AstrBotDevs/AstrBot)
- [AstrBot 官方文档](https://docs.astrbot.app/)
- [AstrBot 会话控制指南](https://docs.astrbot.app/dev/star/guides/session-control.html)
- [牛客网](https://www.nowcoder.com/)

---

## License

MIT License
