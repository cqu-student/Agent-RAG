# Agent-RAG

> **Agentic RAG 技术综述** — 系统梳理检索增强生成（RAG）从基础范式到前沿 Agentic RAG 的核心技术与进展。

本仓库维护并持续更新 Agentic RAG 及其相关领域的综述文档，涵盖 RAG 基础知识、范式演进、核心检索技术、GraphRAG、Agentic RAG、多模态 RAG、评估方法和应用场景。

完整综述参见：[检索增强生成 (RAG) 技术综述 - Yue Shui](https://syhya.github.io/zh/posts/2025-02-03-rag/)

---

## 目录

- [RAG 基础](#rag-基础)
- [RAG 范式演进](#rag-范式演进)
- [核心检索技术](#核心检索技术)
- [Agentic RAG](#agentic-rag)
- [GraphRAG](#graphrag)
- [多模态 RAG](#多模态-rag)
- [评估方法](#评估方法)
- [应用场景](#应用场景)
- [参考文献](#参考文献)

---

## RAG 基础

检索增强生成（RAG）由 [Lewis et al. (2020)](https://arxiv.org/abs/2005.11401) 首次提出，将参数化记忆（LLM 参数）与非参数化记忆（外部检索）结合，解决 LLM 的知识截止性、幻觉、领域知识缺乏等问题。

基本流程：**数据处理与索引 → 检索 → 生成**

### RAG vs 微调

| 特性 | RAG | 模型微调 |
|------|-----|---------|
| 知识更新 | 近实时 | 需重新训练 |
| 成本 | 推理有检索开销 | 训练成本高 |
| 可解释性 | 可追溯来源 | 较低 |

---

## RAG 范式演进

### 朴素 RAG (Naive RAG)
"索引 → 检索 → 生成"线性流程；局限性包括检索质量低、幻觉、上下文整合不佳。

### 高级 RAG (Advanced RAG)
- **预检索优化:** 数据清洗、查询扩展 ([Jagerman et al., 2023](https://arxiv.org/abs/2305.03653))、查询重写 ([Ma et al., 2023](https://arxiv.org/abs/2305.14283))、HyDE ([Gao et al., 2023](https://arxiv.org/abs/2212.10496))
- **检索中优化:** 混合检索 (BM25 + 向量)、嵌入模型微调 ([BGE M3](https://arxiv.org/abs/2402.03216))
- **后检索优化:** 重排序 (Cross-Encoder)、上下文压缩 ([LLMLingua](https://arxiv.org/abs/2310.05736), [RECOMP](https://arxiv.org/abs/2310.04408))

### 模块化 RAG (Modular RAG)
可插拔的核心模块（搜索、记忆、融合、路由等），支持灵活的交互模式。

关键工作：[Self-RAG](https://arxiv.org/abs/2310.11511) · [FLARE](https://arxiv.org/abs/2305.06983) · [RAPTOR](https://arxiv.org/abs/2401.18059) · [CRAG](https://arxiv.org/abs/2401.15884) · [AdaptiveRAG](https://arxiv.org/abs/2403.14403)

---

## 核心检索技术

| 技术 | 描述 | 代表方法 |
|------|------|---------|
| 全文检索 | 基于词频的稀疏检索 | BM25 |
| 向量搜索 | 稠密语义检索 + ANN 索引 | HNSW, FAISS |
| 混合搜索 | BM25 + 向量融合 | RRF |
| 重排序 | 召回后二次精排 | Cross-Encoder, Cohere Rerank |

---

## Agentic RAG

[Agentic RAG](https://arxiv.org/abs/2501.09136) 将自主代理集成到 RAG 流程中，赋予系统动态决策、规划、工具使用和多代理协作能力。

### 架构形态
- **单代理 (Router):** 中心化代理管理全流程
- **多代理 (Multi-Agent):** 多代理分工协作（查询理解、检索、融合、生成）
- **分层代理 (Hierarchical):** 高层规划/分解，低层执行

### 核心机制
- [CRAG](https://arxiv.org/abs/2401.15884): 检索结果自我纠正
- [AdaptiveRAG](https://arxiv.org/abs/2403.14403): 按复杂度动态选择策略
- [Self-RAG](https://arxiv.org/abs/2310.11511): 生成时自主决策检索并自我批判

### 前沿进展
- [Search-R1](https://arxiv.org/abs/2503.09516): RL 训练 LLM 自主搜索
- [R1-Searcher](https://arxiv.org/abs/2503.05592): 纯 RL 教会 LLM 自主调用搜索
- [Search-o1](https://arxiv.org/abs/2501.05366): Agentic RAG 集成到推理模型
- [CoRAG](https://arxiv.org/abs/2501.14342): 训练模型生成中间检索链

---

## GraphRAG

[GraphRAG](https://arxiv.org/abs/2404.16130) 通过构建知识图谱捕捉实体间的复杂关系，支持全局性问题回答。

核心流程：LLM 提取实体/关系 → 社区检测 → 分层摘要 → Map-Reduce 式全局答案生成

---

## 多模态 RAG

[多模态 RAG](https://arxiv.org/abs/2502.08826) 将 RAG 扩展到文本、图像、音频、视频等多种模态。

关键技术：跨模态检索 (CLIP, ColPali) · 多模态融合 · 自适应检索

前沿：[ViDoRAG](https://arxiv.org/abs/2502.18017) · [MegaRAG](https://arxiv.org/abs/2512.20626) · [M3DocRAG](https://arxiv.org/abs/2411.04952)

---

## 评估方法

### Ragas 框架
| 指标 | 定义 |
|------|------|
| Faithfulness | 答案是否完全基于上下文 |
| Answer Relevance | 答案与问题的相关程度 |
| Context Precision | 相关块是否排在前面 |
| Context Recall | 检索是否覆盖答案所需信息 |

### 其他框架与基准
[ARES](https://arxiv.org/abs/2311.09476) · [RGB](https://arxiv.org/abs/2309.01431) · [CRUD-RAG](https://arxiv.org/abs/2401.17043) · [SafeRAG](https://arxiv.org/abs/2501.18636) · [BEIR](https://arxiv.org/abs/2104.08663) · [MTEB](https://arxiv.org/abs/2210.07316)

---

## 应用场景

| 场景 | 代表性工作 |
|------|-----------|
| 开放域问答 | DrQA |
| 医疗 | REALM |
| 法律 | ChatLaw |
| 金融 | AlphaFin |
| 对话系统 | BlenderBot 3 |
| 代码生成 | DocPrompting |
| 推荐系统 | CoRAL |

---

## 参考文献

1. Lewis, P., et al. [*Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.*](https://arxiv.org/abs/2005.11401) NeurIPS 2020.
2. Gao, Y., et al. [*Retrieval-Augmented Generation for Large Language Models: A Survey.*](https://arxiv.org/abs/2312.10997) arXiv 2023.
3. **Yue Shui.** [*检索增强生成 (RAG) 技术综述.*](https://syhya.github.io/zh/posts/2025-02-03-rag/) 2025.
4. Singh, A., et al. [*Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG.*](https://arxiv.org/abs/2501.09136) arXiv 2025.
5. Edge, D., et al. [*From Local to Global: A Graph RAG Approach to Query-Focused Summarization.*](https://arxiv.org/abs/2404.16130) arXiv 2024.
6. Abootorabi, M. M., et al. [*A Survey on Multimodal Retrieval Augmented Generation.*](https://arxiv.org/abs/2502.08826) arXiv 2025.
7. Asai, A., et al. [*Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection.*](https://arxiv.org/abs/2310.11511) ICLR 2024.
8. Yan, S., et al. [*Corrective Retrieval Augmented Generation.*](https://arxiv.org/abs/2401.15884) arXiv 2024.
9. Jin, B., et al. [*Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning.*](https://arxiv.org/abs/2503.09516) arXiv 2025.
10. Peng, H., et al. [*Graph Retrieval-Augmented Generation: A Survey.*](https://arxiv.org/abs/2408.08921) arXiv 2024.
