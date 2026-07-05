# Agent-RAG

> **Agentic RAG 技术综述与实现** — 系统梳理检索增强生成（RAG）及其向智能体（Agent）方向演进的范式、核心技术与前沿进展。

---

## 项目简介

本项目旨在深入研究 **Agentic RAG**（基于智能体的检索增强生成），涵盖从传统 RAG 到多智能体协作、图增强检索、多模态 RAG 等前沿方向的技术综述与工程实现。

RAG 技术已从最初的"索引 → 检索 → 生成"线性流程，逐步演进为具备**动态决策、自主规划、自我反思、工具使用**能力的智能体范式。Agentic RAG 将 AI Agent 的能力（反思、规划、工具调用、多智能体协作）引入检索增强生成流程，是当前 RAG 领域的前沿方向。

---

## 技术全景

### RAG 范式演进

| 范式 | 特征 | 代表工作 |
|------|------|----------|
| **朴素 RAG** | 索引 → 检索 → 生成的线性流程 | [Lewis et al., 2020](https://arxiv.org/abs/2005.11401) |
| **高级 RAG** | 查询扩展、混合检索、重排序、上下文压缩 | [BGE M3](https://arxiv.org/abs/2402.03216), [LLMLingua](https://arxiv.org/abs/2310.05736) |
| **模块化 RAG** | 可插拔模块：搜索、记忆、路由、预测等 | [Self-RAG](https://arxiv.org/abs/2310.11511), [CRAG](https://arxiv.org/abs/2401.15884), [RAPTOR](https://arxiv.org/abs/2401.18059) |
| **Agentic RAG** | 智能体驱动：反思、规划、工具使用、多智能体协作 | [Search-R1](https://arxiv.org/abs/2503.09516), [CoRAG](https://arxiv.org/abs/2501.14342), [GeAR](https://arxiv.org/abs/2412.18431) |

### 关键技术方向

- **Agentic RAG** — 单智能体 / 多智能体 / 分层智能体架构，含反思、规划、工具调用能力
- **GraphRAG** — 基于知识图谱的检索增强，支持全局性复杂问答
- **多模态 RAG** — 跨文本、图像、音频、视频的统一检索与生成
- **评估体系** — Ragas 框架、ARES、RGB、CRUD-RAG、SafeRAG 等

### 核心技术栈

| 层级 | 技术 |
|------|------|
| 检索 | BM25、HNSW、FAISS、混合搜索（RRF）、Cross-Encoder 重排序 |
| 嵌入 | BGE M3、CLIP、ColPali |
| 智能体 | Self-Refine、Reflexion、AutoGen、Toolformer |
| 图检索 | Microsoft GraphRAG、G-Retriever、HippoRAG 2 |
| 评估 | Ragas、ARES、RGB、BEIR、KILT、MTEB |

---

## 目录结构

```
Agent-RAG/
├── README.md              # 项目概述（本文档）
├── docs/
│   └── survey.md          # Agentic RAG 技术综述（详细）
└── .github/
    └── workflows/
        └── opencode.yml   # CI 工作流
```

---

## 技术综述

详细的技术综述文档请参阅 [docs/survey.md](docs/survey.md)，涵盖以下内容：

1. **RAG 基础** — 核心概念、三段式流程、RAG vs 微调 vs 长上下文对比
2. **RAG 范式演进** — 朴素 RAG → 高级 RAG → 模块化 RAG → Agentic RAG
3. **核心检索技术** — 全文检索、向量搜索、混合搜索、重排序
4. **Agentic RAG** — 架构形态（单/多/分层智能体）、核心机制（CRAG/AdaptiveRAG/Self-RAG）、前沿进展（Search-R1/R1-Searcher/Search-o1/CoRAG/GeAR）
5. **GraphRAG** — 知识图谱构建、社区检测、分层摘要
6. **多模态 RAG** — 跨模态检索、多模态融合、ViDoRAG/MegaRAG/M3DocRAG
7. **评估方法** — Ragas 框架、ARES、RGB、CRUD-RAG、SafeRAG、通用基准
8. **应用场景** — 开放域问答、医疗、法律、金融、对话、代码生成、推荐系统、科学研究

---

## 路线图

- [x] Agentic RAG 技术综述文档
- [ ] 基础 RAG Pipeline 实现
- [ ] 高级检索模块（混合搜索、重排序）
- [ ] CRAG / Self-RAG / AdaptiveRAG 核心机制复现
- [ ] 单智能体 / 多智能体 RAG 系统
- [ ] GraphRAG 集成
- [ ] 多模态 RAG 支持
- [ ] 完整评估体系

---

## 参考文献

关键文献：

1. Lewis, P., et al. [*RAG for Knowledge-Intensive NLP Tasks*](https://arxiv.org/abs/2005.11401). NeurIPS 2020.
2. Singh, A., et al. [*Agentic RAG: A Survey on Agentic RAG*](https://arxiv.org/abs/2501.09136). arXiv 2025.
3. Edge, D., et al. [*From Local to Global: A Graph RAG Approach*](https://arxiv.org/abs/2404.16130). arXiv 2024.
4. Asai, A., et al. [*Self-RAG: Learning to Retrieve, Generate, and Critique*](https://arxiv.org/abs/2310.11511). ICLR 2024.
5. Jin, B., et al. [*Search-R1: Training LLMs to Reason and Leverage Search Engines with RL*](https://arxiv.org/abs/2503.09516). arXiv 2025.
6. Wang, L., et al. [*CoRAG: Chain-of-Retrieval Augmented Generation*](https://arxiv.org/abs/2501.14342). arXiv 2025.

完整参考文献请参见 [docs/survey.md](docs/survey.md)。

---

## 许可

本项目仅供学习和研究使用。
