# Context & Memory Research

**Status:** ACTIVE  
**Created:** 2026-03-04  
**Owner:** Luna 🌙  
**GitHub:** https://github.com/openclaw/context-memory-research

## 概述

AI Agent 的上下文管理與記憶系統研究專案。這是一個持續更新的知識庫，追蹤業界最新發展、架構設計、以及 OpenClaw 的實作方向。

## 研究範疇

### 1. Memory Architecture（記憶架構）
- Multi-tiered memory systems（分層記憶）
- Working / Episodic / Semantic / Procedural memory
- Vector DB vs Agentic Search
- File-based vs Database-backed

### 2. Context Engineering（上下文工程）
- Context window management
- Compression & summarization
- Selective context injection
- Context isolation in multi-agent systems

### 3. Implementations（實作案例）
- **MemGPT / Letta** — LLM-OS paradigm, self-editing memory
- **ByteRover** — Context Tree, Agentic Search
- **OpenClaw** — MEMORY.md + daily logs + memory_search
- **Claude Memory** — Anthropic's approach
- **Cursor / Windsurf** — IDE context management

### 4. OpenClaw 改進方向
- 我們目前的架構 vs 業界最佳實踐
- 可能的改進：topic-based memory, auto-consolidation, memory versioning

## Tasks

- [x] T001: 收集 ByteRover memory architecture 筆記
- [ ] T002: 深入研究 MemGPT/Letta 架構
- [ ] T003: 研究 Claude Memory 系統
- [ ] T004: 整理 Context Engineering 最佳實踐
- [ ] T005: 建立 GitHub repo 並同步
- [ ] T006: 設計 OpenClaw memory improvement roadmap

## 參考資源

### 文章
- [ByteRover CLI 2.0 Architecture](https://www.byterover.dev/blog/memory-architecture)
- [Memory for AI Agents - The New Stack](https://thenewstack.io/memory-for-ai-agents-a-new-paradigm-of-context-engineering/)
- [Letta Agent Memory Blog](https://www.letta.com/blog/agent-memory)
- [Building AI Agents That Remember - TowardsAI](https://pub.towardsai.net/building-ai-agents-that-actually-remember-a-deep-dive-into-memory-architectures-db79a15dba70)

### 論文 / 深度資源
- [MemGPT Paper](https://arxiv.org/abs/2310.08560)
- [Memory Architectures in Long-Term AI Agents - ResearchGate](https://www.researchgate.net/publication/388144017)

### 工具 / 框架
- [Letta (MemGPT)](https://github.com/letta-ai/letta)
- [LangChain Memory](https://python.langchain.com/docs/modules/memory/)
- [Cipher Framework](https://docs.byterover.dev/cipher/memory-overview)

---
*This is a living document. Updated as research progresses.*
