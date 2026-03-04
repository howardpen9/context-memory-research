# Context Engineering

> Context management 不再是小細節，是 **primary engineering challenge**。

## 為什麼重要？

1. **Context window 有限** — 即使 1M tokens，實際有效使用率有限
2. **長 context = 高成本** — Token 費用隨 context 線性增長
3. **長 context = 性能下降** — "Lost in the middle" 問題
4. **Quality > Quantity** — 精準的 context 勝過大量雜訊

## 核心策略

### 1. Selective Context Injection

只注入當前任務最相關的資訊。

```
❌ 錯誤做法：把整個 codebase 塞進 context
✅ 正確做法：根據任務動態選擇相關檔案
```

#### 技術手段
- **Semantic search**: 用 embeddings 找相關內容
- **Keyword extraction**: 從問題提取關鍵詞
- **Dependency analysis**: 追蹤程式碼依賴關係
- **Recency weighting**: 最近的資訊權重更高

### 2. Compression & Summarization

壓縮資訊，保留核心。

#### 層次壓縮
```
Full conversation (10K tokens)
    ↓ Summarize
Key points (500 tokens)
    ↓ Further compress
Critical facts (50 tokens)
```

#### 策略
- **Progressive summarization**: 隨時間逐漸壓縮舊資訊
- **Hierarchical summaries**: 不同粒度的摘要
- **Lossy compression**: 接受某些資訊遺失

### 3. Strategic Forgetting

主動遺忘不重要的資訊。

```python
# 遺忘策略
def should_forget(memory):
    if memory.age > 30_days and memory.access_count < 2:
        return True
    if memory.relevance_score < 0.3:
        return True
    return False
```

#### 考量因素
- **Time decay**: 時間越久，重要性越低
- **Access frequency**: 很少被存取的資訊
- **Relevance to current context**: 與當前任務無關
- **Redundancy**: 已被更新版本取代

### 4. Context Isolation

在 multi-agent 系統中隔離 context。

```
┌─────────────────┐  ┌─────────────────┐
│  Agent A        │  │  Agent B        │
│  ┌───────────┐  │  │  ┌───────────┐  │
│  │ Context A │  │  │  │ Context B │  │
│  └───────────┘  │  │  └───────────┘  │
└─────────────────┘  └─────────────────┘
         ↓                    ↓
    ┌─────────────────────────────────┐
    │     Shared Knowledge Base       │
    └─────────────────────────────────┘
```

#### 好處
- 避免 context pollution
- 每個 agent 專注自己的任務
- 減少單一 agent 的 context 負擔

### 5. Offloading

大型資料存外部，只給 reference。

```
❌ 塞入整份文件 (100K tokens)
✅ 存入外部，context 只放 metadata + summary (500 tokens)
```

## 常見問題與解法

| 問題 | 描述 | 解法 |
|-----|------|-----|
| Context Rot | 舊資訊累積導致效能下降 | Periodic pruning, summarization |
| Lost in the Middle | 長 context 中間資訊被忽略 | Strategic positioning, chunking |
| Information Fragmentation | 相關資訊分散各處 | Consolidation, linking |
| Stale Data | 過時資訊誤導 agent | Timestamp tracking, invalidation |

## Practical Patterns

### Pattern 1: Sliding Window + Summary

```
[Summary of older context]
[Recent N messages in full]
[Current user input]
```

### Pattern 2: Layered Context

```
[System prompt - always present]
[Relevant knowledge - dynamically loaded]
[Recent conversation - sliding window]
[Current task context]
```

### Pattern 3: RAG with Filtering

```
Query → Retrieve top-K → Filter by relevance → Inject
```

## OpenClaw 的 Context Engineering

### 現有機制
- `memory_search` — 語意搜索 MEMORY.md + daily logs
- Project context injection — 載入相關專案檔案
- Skills — 按需載入特定能力

### 可能改進
1. **Auto-summarization** — 自動壓縮舊對話
2. **Smart context loading** — 根據任務動態選擇載入什麼
3. **Context budget** — 設定 token 上限，強制優先級

---

*Last updated: 2026-03-04*
