# Agentic RAG 技术综述

> **本文档持续更新中**，旨在系统梳理 Agentic RAG 及其相关领域的核心技术、范式演进与前沿进展。

---

## 目录

- [1. RAG 基础](#1-rag-基础)
- [2. RAG 范式演进](#2-rag-范式演进)
  - [2.1 朴素 RAG (Naive RAG)](#21-朴素-rag-naive-rag)
  - [2.2 高级 RAG (Advanced RAG)](#22-高级-rag-advanced-rag)
  - [2.3 模块化 RAG (Modular RAG)](#23-模块化-rag-modular-rag)
- [3. 核心检索技术](#3-核心检索技术)
- [4. Agentic RAG](#4-agentic-rag)
  - [4.1 架构形态](#41-架构形态)
  - [4.2 核心机制](#42-核心机制)
  - [4.3 前沿进展](#43-前沿进展)
- [5. GraphRAG](#5-graphrag)
- [6. 多模态 RAG](#6-多模态-rag)
- [7. 评估方法](#7-评估方法)
- [8. 应用场景](#8-应用场景)
- [9. 参考文献](#9-参考文献)

---

## 1. RAG 基础

检索增强生成（Retrieval-Augmented Generation, RAG）由 [Lewis et al. (2020)](https://arxiv.org/abs/2005.11401) 首次系统提出，旨在将参数化记忆（语言模型参数）与非参数化记忆（外部检索语料）结合，解决 LLM 固有的知识截止性、幻觉、领域知识缺乏等问题。

RAG 的基本流程包含三个阶段：

- **数据处理与索引 (Indexing):** 文档加载 → 文本分块 (Chunking) → 文本嵌入 (Embedding) → 向量存储与索引
- **检索 (Retrieval):** 查询嵌入 → 相似性搜索 → 上下文选择 (Top-K)
- **生成 (Generation):** 提示构建 → LLM 推理 → 答案输出

> 详细的 RAG 基础知识、技术定位（与微调对比）、完整流程说明，参见综述：[检索增强生成 (RAG) 技术综述 - Yue Shui](https://syhya.github.io/zh/posts/2025-02-03-rag/) (2025)

### RAG vs 微调 vs 长上下文

| 特性 | RAG | 模型微调 | 长上下文 |
|------|-----|---------|---------|
| 知识更新 | 近实时 | 需重新训练 | 依赖上下文填充 |
| 成本 | 推理有检索开销 | 训练成本高 | 推理成本随长度增长 |
| 可解释性 | 可追溯来源 | 较低 | 取决于模型 |
| 适用场景 | 动态知识、私有知识 | 学习风格/格式 | 少量长文档整体理解 |

---

## 2. RAG 范式演进

### 2.1 朴素 RAG (Naive RAG)

遵循"索引 → 检索 → 生成"的线性流程。主要局限性包括检索质量低、生成幻觉、上下文整合不佳。

### 2.2 高级 RAG (Advanced RAG)

优化检索和生成过程：

- **预检索:** 数据清洗、元数据增强、查询扩展 ([Jagerman et al., 2023](https://arxiv.org/abs/2305.03653))、查询重写 ([Ma et al., 2023](https://arxiv.org/abs/2305.14283))、HyDE ([Gao et al., 2023](https://arxiv.org/abs/2212.10496))
- **检索中:** 混合检索 (BM25 + 向量搜索)、嵌入模型微调 ([BGE M3, Chen et al., 2024](https://arxiv.org/abs/2402.03216))
- **后检索:** 重排序 (Cross-Encoder)、上下文压缩 ([LLMLingua, Jiang et al., 2023](https://arxiv.org/abs/2310.05736); [RECOMP, Xu et al., 2024](https://arxiv.org/abs/2310.04408))

### 2.3 模块化 RAG (Modular RAG)

将 RAG 系统拆分为可插拔的核心模块：搜索、记忆、融合、路由、预测、任务适配器等，支持灵活的交互模式（迭代检索、自适应检索、递归检索等）。

- **Self-RAG** ([Asai et al., 2024](https://arxiv.org/abs/2310.11511)): LLM 在生成时动态决策是否检索，引入批判令牌
- **FLARE** ([Jiang et al., 2023](https://arxiv.org/abs/2305.06983)): 主动检索，根据生成置信度触发
- **RAPTOR** ([Sarthi et al., 2024](https://arxiv.org/abs/2401.18059)): 递归聚类 + 摘要构建树状索引
- **CRAG** ([Yan et al., 2024](https://arxiv.org/abs/2401.15884)): 检索结果自我纠正机制
- **AdaptiveRAG** ([Jeong et al., 2024](https://arxiv.org/abs/2403.14403)): 按查询复杂度动态选择策略

---

## 3. 核心检索技术

| 技术 | 描述 | 代表方法 |
|------|------|---------|
| 全文检索 | 基于词频的稀疏检索 | BM25 ([Robertson & Zaragoza, 2009](https://ir.webis.de/anthology/2009.ftir_journal-ir0anthology0volumeA3A4.0/)) |
| 向量搜索 | 稠密语义检索 + ANN 索引 | HNSW ([Malkov & Yashunin, 2020](https://arxiv.org/abs/1603.09320)), FAISS ([Johnson et al., 2019](https://arxiv.org/abs/1702.08734)) |
| 混合搜索 | BM25 + 向量搜索融合 | RRF ([Cormack et al., 2009](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf)) |
| 重排序 | 召回后二次精排 | Cross-Encoder, Cohere Rerank, bge-reranker |

---

## 4. Agentic RAG

**Agentic RAG** ([Singh et al., 2025](https://arxiv.org/abs/2501.09136)) 是 RAG 的前沿范式，将自主代理（AI Agents）集成到 RAG 流程中，赋予系统动态决策、规划、工具使用和多代理协作能力。

核心代理能力：
- **反思 (Reflection):** 评估和迭代改进输出 ([Self-Refine, Madaan et al., 2023](https://arxiv.org/abs/2303.17651); [Reflexion, Shinn et al., 2023](https://arxiv.org/abs/2303.11366))
- **规划 (Planning):** 分解复杂任务为子任务
- **工具使用 (Tool Use):** 调用外部工具/API ([Toolformer, Schick et al., 2023](https://arxiv.org/abs/2302.04761))
- **多代理协作 (Multi-Agent):** 多代理分工协作 ([AutoGen, Wu et al., 2023](https://arxiv.org/abs/2308.08155))

### 4.1 架构形态

| 架构 | 特点 | 适用场景 |
|------|------|---------|
| 单代理 (Router) | 中心化代理管理全流程 | 任务明确、工具集有限 |
| 多代理 (Multi-Agent) | 多代理分工（查询理解、检索、融合、生成） | 多数据源、复杂流程 |
| 分层代理 (Hierarchical) | 高层规划/分解，低层执行 | 多步骤推理、复杂决策 |

### 4.2 核心机制

- **纠正性 RAG (CRAG)** ([Yan et al., 2024](https://arxiv.org/abs/2401.15884)): 评估检索质量 → 触发补充检索或筛选
- **自适应 RAG (AdaptiveRAG)** ([Jeong et al., 2024](https://arxiv.org/abs/2403.14403)): 按复杂度选择无检索/单次/多轮策略
- **Self-RAG** ([Asai et al., 2024](https://arxiv.org/abs/2310.11511)): 生成时自主决策检索并自我批判

### 4.3 前沿进展

- **Search-R1** ([Jin et al., 2025](https://arxiv.org/abs/2503.09516)): 用 RL 训练 LLM 在推理过程中自主搜索，引入 retrieved token masking 实现稳定 RL 训练
- **R1-Searcher** ([Song et al., 2025](https://arxiv.org/abs/2503.05592)): 纯 RL 方法教会 LLM 自主调用搜索，无需过程奖励或蒸馏
- **Search-o1** ([Li et al., 2025](https://arxiv.org/abs/2501.05366)): 将 Agentic RAG 集成到大型推理模型中，含 Reason-in-Documents 模块减少检索噪声
- **CoRAG** ([Wang et al., 2025](https://arxiv.org/abs/2501.14342)): 训练模型生成中间检索链，实现逐步检索与推理
- **Agent-G** ([Lee et al., 2024](https://openreview.net/forum?id=g2C947jjjQ)): 基于代理的图检索框架，多代理动态分工
- **GeAR** ([Shen et al., 2024](https://arxiv.org/abs/2412.18431)): 图扩展增强检索器，处理多跳查询

---

## 5. GraphRAG

**GraphRAG** ([Edge et al., 2024](https://arxiv.org/abs/2404.16130); [GitHub](https://github.com/microsoft/graphrag)) 通过构建知识图谱捕捉实体间的复杂关系，支持全局性问题的回答。

核心流程：
1. LLM 提取实体/关系 → 构建知识图谱
2. 社区检测 (Leiden 算法) → 分层社区摘要
3. Map-Reduce 式全局答案生成

其他方法：
- **G-Retriever** ([He et al., 2024](https://arxiv.org/abs/2402.07630)): 文本图理解与问答
- **HippoRAG 2** ([Gutierrez et al., 2025](https://arxiv.org/abs/2502.14802)): 将 RAG 推向类人长期记忆系统
- **GraphRAG 综述** ([Peng et al., 2024](https://arxiv.org/abs/2408.08921))

---

## 6. 多模态 RAG

**多模态 RAG** ([Abootorabi et al., 2025](https://arxiv.org/abs/2502.08826); [Zhao et al., 2023](https://arxiv.org/abs/2309.15564)) 将 RAG 扩展到文本、图像、音频、视频等多种模态。

关键技术：
- **跨模态检索:** CLIP ([Radford et al., 2021](https://arxiv.org/abs/2103.00020)), ColPali ([Faysse et al., 2024](https://arxiv.org/abs/2407.01449))
- **多模态融合:** 统一框架投影、跨注意力机制
- **自适应检索:** OmniSearch ([Li et al., 2024](https://arxiv.org/abs/2411.02937)), SKURG ([Yang et al., 2022](https://arxiv.org/abs/2212.08632))

前沿进展：
- **ViDoRAG** ([Wang et al., 2025](https://arxiv.org/abs/2502.18017)): 视觉文档多智能体 RAG，GMM 混合检索 + 迭代工作流
- **MegaRAG** ([Hsiao et al., 2025](https://arxiv.org/abs/2512.20626)): 多模态知识图谱 RAG
- **M3DocRAG** ([Cho et al., 2024](https://arxiv.org/abs/2411.04952)): 多页文档展平嵌入

---

## 7. 评估方法

### 7.1 Ragas 框架 ([Es et al., 2023](https://arxiv.org/abs/2309.15217))

| 指标 | 定义 | 依赖 GT |
|------|------|--------|
| Faithfulness | 答案是否完全基于上下文 | 否 |
| Answer Relevance | 答案与问题的相关程度 | 否 |
| Context Precision | 相关块是否排在前面 | 否 |
| Context Recall | 检索是否覆盖答案所需信息 | 是 |
| Answer Semantic Similarity | 生成答案与标准答案的语义相似度 | 是 |
| Answer Correctness | 事实层面的正确性 | 是 |

### 7.2 其他评估框架

- **ARES** ([Saad-Falcon et al., 2023](https://arxiv.org/abs/2311.09476)): LLM 合成数据评估
- **RGB** ([Chen et al., 2024](https://arxiv.org/abs/2309.01431)): 噪声鲁棒性、负例拒绝、信息整合
- **CRUD-RAG** ([Lyu et al., 2024](https://arxiv.org/abs/2401.17043)): 中文 RAG 基准
- **SafeRAG** ([Liang et al., 2025](https://arxiv.org/abs/2501.18636)): RAG 安全性基准
- **ClashEval** ([Wu et al., 2024](https://arxiv.org/abs/2404.10198)): 知识冲突评估

### 7.3 通用基准

- **BEIR** ([Thakur et al., 2021](https://arxiv.org/abs/2104.08663)): 信息检索基准
- **KILT** ([Petroni et al., 2020](https://arxiv.org/abs/2009.02252)): 知识密集型任务基准
- **MTEB** ([Muennighoff et al., 2022](https://arxiv.org/abs/2210.07316)): 文本嵌入模型基准

---

## 8. 应用场景

| 场景 | 代表性工作 |
|------|-----------|
| 开放域问答 | DrQA ([Chen et al., 2017](https://arxiv.org/abs/1704.00051)) |
| 医疗 | REALM ([Zhu et al., 2024](https://arxiv.org/abs/2402.07016)) |
| 法律 | ChatLaw ([Cui et al., 2023](https://arxiv.org/abs/2306.16092)) |
| 金融 | AlphaFin ([Zhang et al., 2024](https://arxiv.org/abs/2403.12582)) |
| 对话系统 | BlenderBot 3 ([Shuster et al., 2022](https://arxiv.org/abs/2208.03188)) |
| 代码生成 | DocPrompting ([Zhou et al., 2022](https://arxiv.org/abs/2207.05987)) |
| 推荐系统 | CoRAL ([Wu et al., 2024](https://arxiv.org/abs/2403.06447)) |
| 科学研究 | MolReGPT ([Li et al., 2023](https://arxiv.org/abs/2306.06615)) |
| 多模态应用 | 视觉问答、视频理解 |

---

## 9. 参考文献

1. Lewis, P., et al. [*Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.*](https://arxiv.org/abs/2005.11401) NeurIPS 2020.
2. Gao, Y., et al. [*Retrieval-Augmented Generation for Large Language Models: A Survey.*](https://arxiv.org/abs/2312.10997) arXiv 2023.
3. Yue Shui. [*检索增强生成 (RAG) 技术综述.*](https://syhya.github.io/zh/posts/2025-02-03-rag/) syhya.github.io, Feb 2025.
4. Singh, A., et al. [*Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG.*](https://arxiv.org/abs/2501.09136) arXiv 2025.
5. Edge, D., et al. [*From Local to Global: A Graph RAG Approach to Query-Focused Summarization.*](https://arxiv.org/abs/2404.16130) arXiv 2024.
6. Abootorabi, M. M., et al. [*A Survey on Multimodal Retrieval Augmented Generation.*](https://arxiv.org/abs/2502.08826) arXiv 2025.
7. Asai, A., et al. [*Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection.*](https://arxiv.org/abs/2310.11511) ICLR 2024.
8. Yan, S., et al. [*Corrective Retrieval Augmented Generation.*](https://arxiv.org/abs/2401.15884) arXiv 2024.
9. Jin, B., et al. [*Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning.*](https://arxiv.org/abs/2503.09516) arXiv 2025.
10. Li, Z., et al. [*RAG vs. Long-Context LLMs: A Comprehensive Study and Hybrid Approach.*](https://arxiv.org/abs/2407.16833) EMNLP 2024.
11. Es, S., et al. [*RAGAS: Automated Evaluation of Retrieval Augmented Generation.*](https://arxiv.org/abs/2309.15217) arXiv 2023.
12. Peng, H., et al. [*Graph Retrieval-Augmented Generation: A Survey.*](https://arxiv.org/abs/2408.08921) arXiv 2024.
13. Zhao, P., et al. [*Retrieving Multimodal Information for Augmented Generation: A Survey.*](https://arxiv.org/abs/2309.15564) EMNLP 2023.
14. Wang, L., et al. [*CoRAG: Chain-of-Retrieval Augmented Generation.*](https://arxiv.org/abs/2501.14342) arXiv 2025.
15. Anthropic. [*Contextual Retrieval.*](https://www.anthropic.com/engineering/contextual-retrieval) 2024.
