# OpenClaw Memory Improvement Roadmap

*研究業界最佳實踐後的改進方向*

## 現狀分析

### 目前架構
```
workspace/
├── MEMORY.md              # Curated long-term memory (手動維護)
├── memory/
│   └── YYYY-MM-DD.md      # Daily logs (raw notes)
└── [memory_search tool]   # Semantic search across memory files
```

### 優點
- ✅ 簡單直觀，human-readable
- ✅ Git-friendly，版本控制內建
- ✅ 適合 1:1 personal assistant
- ✅ Agent 可直接編輯（self-editing）
- ✅ 零依賴，純 markdown

### 限制
- ⚠️ 需要手動維護 MEMORY.md
- ⚠️ 無 topic-based 結構
- ⚠️ 無 memory diff preview
- ⚠️ 無 automatic consolidation

## 改進方向

### Phase 1: Auto-Consolidation（自動整合）

**目標**: Heartbeat 時自動 review daily logs → 更新 MEMORY.md

```
daily logs (raw)
    ↓ [Agent reviews during heartbeat]
MEMORY.md (curated)
```

**實作**:
- 在 HEARTBEAT.md 加入 memory review 週期（每 3 天）
- Agent 讀取最近 3 天 daily logs
- 識別重要事件、決定、lessons
- 更新 MEMORY.md

**狀態**: ✅ 已有類似機制，需要更系統化

### Phase 2: Topic-Based Organization（主題分類）

**目標**: 類似 ByteRover 的 Context Tree

```
memory/
├── YYYY-MM-DD.md          # Daily logs (keep)
├── topics/
│   ├── projects.md        # 專案相關記憶
│   ├── people.md          # 人物相關
│   ├── decisions.md       # 重要決定
│   └── lessons.md         # 學到的教訓
```

**優點**:
- 更易於 targeted retrieval
- 減少單一 MEMORY.md 過大
- Agent 可以只載入相關 topic

**考量**:
- 增加複雜度
- 需要 agent 判斷分類
- 可能 overkill for personal use

### Phase 3: Memory Diff Preview

**目標**: 修改 MEMORY.md 前先預覽變動

```bash
# 概念
luna memory diff     # 顯示建議的 MEMORY.md 更新
luna memory apply    # 套用更新
luna memory rollback # 回滾到之前版本
```

**實作選項**:
- OpenClaw CLI 新增 memory 子命令
- 或讓 agent 在 edit 前先展示 diff

### Phase 4: Smarter Retrieval

**目標**: 類似 Agentic Search

**現狀**: `memory_search` 用 semantic search

**改進**:
- Task-aware retrieval（根據當前任務調整搜索）
- Relevance scoring with context
- Multi-hop reasoning（找到 A，再從 A 找相關的 B）

### Phase 5: Multi-Agent Memory Sharing

**目標**: Luna 的 sub-agents 可以共享某些 memory

```
Luna (主 agent)
├── Private memory (MEMORY.md)
└── Shared knowledge base
    ↑
    ├── Shuri 可讀
    ├── Friday 可讀
    └── etc.
```

**考量**:
- 安全性：什麼可以共享？
- 一致性：誰可以寫？
- 目前 sub-agents 是 ephemeral，需要持久化嗎？

## 優先級建議

| Phase | 難度 | 價值 | 建議 |
|-------|-----|-----|------|
| 1. Auto-Consolidation | 低 | 高 | ⭐ 先做 |
| 2. Topic Organization | 中 | 中 | 觀察需求再說 |
| 3. Memory Diff | 中 | 中 | Nice to have |
| 4. Smarter Retrieval | 高 | 高 | 需要 OpenClaw core 改動 |
| 5. Multi-Agent Sharing | 高 | 中 | 等需求更明確 |

## 不做什麼

基於研究，以下**暫時不需要**：

- ❌ Vector DB — 對個人使用 overkill，markdown + semantic search 夠用
- ❌ Knowledge Graph — 複雜度太高，ROI 不明確
- ❌ Database-backed storage — 失去 git-friendly 優勢

## 下一步

1. 加強 HEARTBEAT.md 的 memory review 機制
2. 實驗 topic 子目錄看是否有幫助
3. 持續追蹤業界發展，更新這份 roadmap

---

*Last updated: 2026-03-04*
