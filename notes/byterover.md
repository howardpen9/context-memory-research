# ByteRover CLI 2.0 Memory Architecture

*Source: https://www.byterover.dev/blog/memory-architecture*

## Overview

ByteRover CLI 2.0 重新設計了 memory architecture，從傳統 Vector DB + similarity search 轉向更結構化、智能化的方式。

## Context Tree（三層結構）

```
Domains (高階分類)
│   例: "Architecture", "API", "Frontend"
│
└─ Topics (具體主題)
    │   例: "Authentication", "Database Schema"
    │
    └─ Context Files (markdown 知識檔案)
        實際存儲知識的地方
```

### 優點
- 比扁平結構更易導航
- Agent 可以先定位 domain，再找 topic
- 適合大型專案的知識組織

## Agentic Search

取代傳統的 Vector DB similarity search。

### 傳統方式
```
Query → Embedding → Vector similarity → Top-K results
```

### Agentic Search
```
Query → Agent 理解意圖 → Task-aware retrieval → Relevant results
```

### 差異
| 傳統 Vector Search | Agentic Search |
|-------------------|----------------|
| 純粹語意相似度 | 任務導向 |
| 可能有 noise | 更精準 |
| 固定 embedding | 動態理解 |

## Memory Version Control

類似 Git 的 memory 版本控制。

```bash
brv push      # 推送 local memory 到 remote
brv pull      # 拉取 remote memory updates
brv diff      # 預覽 memory 變動
brv rollback  # 回滾到之前版本
```

### 用途
- 團隊協作共享 memory
- 實驗性修改可回滾
- Memory 變更歷史追蹤

## Context Composer

從現有文件自動萃取 memory。

### 流程
1. 輸入：rules, PRDs, guidelines, best practices
2. AI 分析文件，提取 key information
3. Chat-like interface 精煉結果
4. 輸出：結構化的 Context Files

## 底層框架：Cipher

ByteRover 建立在 open-source Cipher framework 上。

### Storage Architecture（四層）
```
┌─────────────────────────────┐
│  Cache Backend (Redis)      │ ← Ephemeral data
├─────────────────────────────┤
│  Database (PostgreSQL)      │ ← Persistent data
├─────────────────────────────┤
│  Vector Storage             │ ← Semantic search
├─────────────────────────────┤
│  Knowledge Graph            │ ← Entity relationships
└─────────────────────────────┘
```

### Memory Types
- **Knowledge Memory**: 事實、技術概念，用 vector embeddings
- **Reflection Memory**: Agent 的推理過程、決策模式

## 對 OpenClaw 的啟發

| ByteRover | OpenClaw 現況 | 可能改進 |
|-----------|--------------|---------|
| Domain/Topic/File | Daily + MEMORY.md | Topic 子目錄 |
| Agentic Search | memory_search | 已類似 ✓ |
| Memory Git | workspace git | Memory diff preview |
| Context Composer | 手動維護 | Auto-consolidate daily → MEMORY |

---

*Last updated: 2026-03-04*
