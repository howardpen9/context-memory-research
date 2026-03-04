# MemGPT / Letta Architecture

*Sources: MemGPT paper, Letta blog, various articles*

## Core Concept: LLM as Operating System

MemGPT 的核心創新：讓 LLM 自己管理 memory，就像 OS 管理 RAM/Disk。

### 為什麼需要？
- LLM context window 有限（即使 1M tokens 也不夠）
- 傳統 LLM 是 stateless，每次對話從零開始
- 需要 persistent, evolving memory

## Memory Hierarchy

```
┌─────────────────────────────────────────┐
│     Main Context (Core Memory)          │
│     ≈ RAM                               │
│                                         │
│  • 高優先級，always in context          │
│  • User preferences, agent persona      │
│  • Customizable "memory blocks"         │
│  • 直接影響 agent 回應                  │
└─────────────────────────────────────────┘
                    ↕ Agent 自主管理
┌─────────────────────────────────────────┐
│    External Context (Archival/Recall)   │
│    ≈ Disk                               │
│                                         │
│  • 大量 searchable archive              │
│  • Past conversations, documents        │
│  • Vector DB (LanceDB) for retrieval    │
└─────────────────────────────────────────┘
```

## Self-Editing Memory

關鍵特性：Agent 透過 **tool calls** 修改自己的 memory。

### 可用的 Memory Tools
```python
# 更新 core memory
memory_replace(section="persona", old="...", new="...")

# 存入 archival memory
archival_memory_insert(content="...")

# 搜索 archival memory
archival_memory_search(query="...")

# 搜索過去對話
conversation_search(query="...")
```

### 運作流程
```
User input
    ↓
Agent 思考：這個資訊重要嗎？
    ↓
決定：Retain / Archive / Ignore
    ↓
呼叫對應 memory tool
    ↓
Memory 更新，影響未來對話
```

## Letta Platform

Letta 是 MemGPT 的產品化版本。

### 架構特點

1. **Persistent State**
   - 所有 agent state 存在 database
   - Message history, memories, tools 都持久化
   - Agent 重啟後保持 identity

2. **Agentic Loop**
   ```
   ┌─────────────────────────────────────┐
   │  LLM generates:                     │
   │  • Internal reasoning (hidden)      │
   │  • Tool calls                       │
   │  • User-facing messages             │
   └─────────────────────────────────────┘
              ↓
   ┌─────────────────────────────────────┐
   │  Agent decides:                     │
   │  • Continue reasoning?              │
   │  • Call tools?                      │
   │  • Send message to user?            │
   └─────────────────────────────────────┘
   ```

3. **Model Agnostic**
   - 支援 GPT-3/4, Claude, 開源模型
   - 統一的 memory interface

4. **ADE (Agent Development Environment)**
   - Visual config and debugging
   - Memory inspection
   - Tool management

## Memory Block 設計

Letta 的 core memory 使用 "blocks" 概念：

```python
# 範例 memory blocks
{
  "persona": "I am Luna, an AI assistant...",
  "human": "Howard is a developer who...",
  "preferences": {
    "language": "Chinese/English mixed",
    "communication_style": "direct, technical"
  }
}
```

Agent 可以動態更新這些 blocks。

## 與 OpenClaw 對比

| 特性 | MemGPT/Letta | OpenClaw |
|-----|-------------|----------|
| Storage | Database + Vector DB | Markdown files + Git |
| Memory editing | Agent tool calls | Agent 手動編輯 MEMORY.md |
| Hierarchy | Core + Archival | MEMORY.md + daily logs |
| Versioning | Database history | Git commits |
| Search | Vector + semantic | memory_search |

### 啟發

1. **Self-editing memory** — OpenClaw 其實已經有，agent 可以 edit MEMORY.md
2. **Memory blocks** — 我們用 sections in MEMORY.md，概念類似
3. **Structured archival** — 可考慮更結構化的 daily log format

---

*Last updated: 2026-03-04*
