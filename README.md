# Context & Memory Research

> 🧠 AI Agent 上下文管理與記憶系統研究

這是一個持續更新的知識庫，追蹤 AI Agent memory architecture 的業界發展、設計模式、以及實作方向。

## 研究範疇

### 1. Memory Architecture（記憶架構）
- Multi-tiered memory systems（分層記憶）
- Working / Episodic / Semantic / Procedural memory
- Vector DB vs Agentic Search
- File-based vs Database-backed storage

### 2. Context Engineering（上下文工程）
- Context window management strategies
- Compression & summarization techniques
- Selective context injection
- Context isolation in multi-agent systems

### 3. Implementations（實作案例）
- **MemGPT / Letta** — LLM-OS paradigm, self-editing memory
- **ByteRover** — Context Tree, Agentic Search
- **OpenClaw** — MEMORY.md + daily logs + semantic search
- **Claude Memory** — Anthropic's approach
- **Cursor / Windsurf** — IDE context management

## 目錄結構

```
├── README.md
├── PROJECT.md           # Project tracking
├── notes/
│   ├── byterover.md      # ByteRover CLI 2.0 架構
│   ├── memgpt-letta.md   # MemGPT/Letta 深度分析
│   ├── context-engineering.md
│   └── ...
├── comparisons/
│   └── architecture-comparison.md
└── openclaw/
    └── improvement-roadmap.md
```

## 參考資源

### 文章
- [ByteRover CLI 2.0 Architecture](https://www.byterover.dev/blog/memory-architecture)
- [Memory for AI Agents - The New Stack](https://thenewstack.io/memory-for-ai-agents-a-new-paradigm-of-context-engineering/)
- [Letta Agent Memory Blog](https://www.letta.com/blog/agent-memory)
- [Building AI Agents That Remember - TowardsAI](https://pub.towardsai.net/building-ai-agents-that-actually-remember-a-deep-dive-into-memory-architectures-db79a15dba70)

### 論文
- [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560)
- [Memory Architectures in Long-Term AI Agents](https://www.researchgate.net/publication/388144017)

### 工具 / 框架
- [Letta (formerly MemGPT)](https://github.com/letta-ai/letta)
- [LangChain Memory](https://python.langchain.com/docs/modules/memory/)
- [Cipher Framework](https://docs.byterover.dev/cipher/memory-overview)

## Contributing

這是 [OpenClaw](https://github.com/openclaw/openclaw) 生態系的研究專案。歡迎 PR 貢獻新的研究筆記或案例分析。

## License

MIT
