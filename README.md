# Awesome Agentic RAG [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> 一份精心策划的 Agentic RAG 资源列表，涵盖检索增强生成（RAG）从基础范式到前沿 Agentic RAG 的核心论文与开源项目。

中文综述参见：[检索增强生成 (RAG) 技术综述 - Yue Shui](https://syhya.github.io/zh/posts/2025-02-03-rag/)

---

## 目录

- [Survey (综述)](#survey-综述)
- [RAG Foundations (RAG 基础)](#rag-foundations-rag-基础)
- [Advanced & Modular RAG (高级与模块化 RAG)](#advanced--modular-rag-高级与模块化-rag)
- [Core Retrieval (核心检索技术)](#core-retrieval-核心检索技术)
- [Agentic RAG (智能体 RAG)](#agentic-rag-智能体-rag)
- [GraphRAG (图 RAG)](#graphrag-图-rag)
- [Multimodal RAG (多模态 RAG)](#multimodal-rag-多模态-rag)
- [Evaluation (评估)](#evaluation-评估)
- [Applications (应用)](#applications-应用)
- [Contributing](#contributing)
- [License](#license)

---

## Survey (综述)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2025-03 | Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning | [Paper](https://arxiv.org/abs/2503.09516) | - | 用 RL 训练 LLM 在推理过程中自主搜索，引入 retrieved token masking 实现稳定 RL 训练 |
| 2025-02 | 检索增强生成 (RAG) 技术综述 | [Paper](https://syhya.github.io/zh/posts/2025-02-03-rag/) | - | Yue Shui. 系统梳理 RAG 基础知识、范式演进、核心技术与前沿进展 |
| 2025-02 | A Survey on Multimodal Retrieval Augmented Generation | [Paper](https://arxiv.org/abs/2502.08826) | - | Abootorabi et al. 多模态 RAG 全面综述 |
| 2025-01 | Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG | [Paper](https://arxiv.org/abs/2501.09136) | - | Singh et al. Agentic RAG 系统综述 |
| 2024-08 | Graph Retrieval-Augmented Generation: A Survey | [Paper](https://arxiv.org/abs/2408.08921) | - | Peng et al. GraphRAG 领域综述 |
| 2023-12 | Retrieval-Augmented Generation for Large Language Models: A Survey | [Paper](https://arxiv.org/abs/2312.10997) | - | Gao et al. RAG 大规模综述 |
| 2023-09 | Retrieving Multimodal Information for Augmented Generation: A Survey | [Paper](https://arxiv.org/abs/2309.15564) | - | Zhao et al. EMNLP 2023. 多模态 RAG 综述 |

---

## RAG Foundations (RAG 基础)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2024-07 | RAG vs. Long-Context LLMs: A Comprehensive Study and Hybrid Approach | [Paper](https://arxiv.org/abs/2407.16833) | - | Li et al. EMNLP 2024. RAG 与长上下文 LLM 的全面对比与混合方法 |
| 2020-05 | Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks | [Paper](https://arxiv.org/abs/2005.11401) | - | Lewis et al. NeurIPS 2020. 首次系统提出 RAG，结合参数化记忆与非参数化记忆 |
| 2020-02 | REALM: Retrieval-Augmented Language Model Pre-Training | [Paper](https://arxiv.org/abs/2002.08909) | - | Guu et al. ICML 2020. 将检索增强引入语言模型预训练 |

---

## Advanced & Modular RAG (高级与模块化 RAG)

### 预检索优化 (Pre-Retrieval)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2023-05 | Query Expansion by Prompting | [Paper](https://arxiv.org/abs/2305.03653) | - | Jagerman et al. 利用 prompt 进行查询扩展 |
| 2023-05 | Query Rewriting for Retrieval-Augmented Large Language Models | [Paper](https://arxiv.org/abs/2305.14283) | - | Ma et al. 查询重写优化检索 |
| 2022-12 | Precise Zero-Shot Dense Retrieval without Relevance Labels (HyDE) | [Paper](https://arxiv.org/abs/2212.10496) | - | Gao et al. 零样本稠密检索，使用假设文档嵌入 |

### 检索中优化 (In-Retrieval)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2024-02 | BGE M3-Embedding: Multi-Lingual, Multi-Functionality, Multi-Granularity Text Embeddings | [Paper](https://arxiv.org/abs/2402.03216) | - | Chen et al. 多语言、多功能、多粒度嵌入模型 |

### 后检索优化 (Post-Retrieval)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2023-10 | LLMLingua: Compressing Prompts for Accelerated Inference | [Paper](https://arxiv.org/abs/2310.05736) | - | Jiang et al. 上下文压缩加速推理 |
| 2023-10 | RECOMP: Improving Retrieval-Augmented LMs with Selective Context Compression | [Paper](https://arxiv.org/abs/2310.04408) | - | Xu et al. 选择性上下文压缩 |

### 模块化 RAG (Modular RAG)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2024-03 | Adaptive-RAG: Learning to Adapt Retrieval-Augmented LLMs via Question Complexity | [Paper](https://arxiv.org/abs/2403.14403) | - | Jeong et al. 按查询复杂度动态选择检索策略 |
| 2024-01 | Corrective Retrieval Augmented Generation (CRAG) | [Paper](https://arxiv.org/abs/2401.15884) | - | Yan et al. 检索结果自我纠正机制 |
| 2024-01 | RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval | [Paper](https://arxiv.org/abs/2401.18059) | - | Sarthi et al. 递归聚类 + 摘要构建树状索引 |
| 2023-10 | Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection | [Paper](https://arxiv.org/abs/2310.11511) | - | Asai et al. ICLR 2024. LLM 生成时自主决策检索并自我批判 |
| 2023-05 | Active Retrieval Augmented Generation (FLARE) | [Paper](https://arxiv.org/abs/2305.06983) | - | Jiang et al. 主动检索，根据生成置信度触发 |

---

## Core Retrieval (核心检索技术)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2020-02 | Efficient and Robust Approximate Nearest Neighbor Search Using HNSW | [Paper](https://arxiv.org/abs/1603.09320) | - | Malkov & Yashunin. 分层可导航小世界图 ANN 索引 |
| 2019-02 | FAISS: A Library for Efficient Similarity Search | [Paper](https://arxiv.org/abs/1702.08734) | [Code](https://github.com/facebookresearch/faiss) | Johnson et al. Meta 开源高效向量相似度搜索库 |
| 2009-07 | Reciprocal Rank Fusion (RRF) | [Paper](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf) | - | Cormack et al. SIGIR 2009. 多排序列表融合算法 |
| 2009-04 | BM25 (Okapi) — The Probabilistic Relevance Framework | [Paper](https://ir.webis.de/anthology/2009.ftir_journal-ir0anthology0volumeA3A4.0/) | - | Robertson & Zaragoza. 经典全文检索排序算法 |

---

## Agentic RAG (智能体 RAG)

Agentic RAG 将自主代理集成到 RAG 流程中，赋予系统动态决策、规划、工具使用和多代理协作能力。

### Agent Frameworks & Capabilities (代理框架与能力)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2023-08 | AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation | [Paper](https://arxiv.org/abs/2308.08155) | [Code](https://github.com/microsoft/autogen) | Wu et al. 多代理对话框架 |
| 2023-03 | Self-Refine: Iterative Refinement with Self-Feedback | [Paper](https://arxiv.org/abs/2303.17651) | - | Madaan et al. 自我反馈迭代改进 |
| 2023-03 | Reflexion: Language Agents with Verbal Reinforcement Learning | [Paper](https://arxiv.org/abs/2303.11366) | - | Shinn et al. 语言代理的口头强化学习 |
| 2023-02 | Toolformer: Language Models Can Teach Themselves to Use Tools | [Paper](https://arxiv.org/abs/2302.04761) | - | Schick et al. LLM 自主学会使用外部工具 |

### Frontier Methods (前沿方法)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2025-03 | Search-R1: Training LLMs to Reason and Leverage Search Engines with Reinforcement Learning | [Paper](https://arxiv.org/abs/2503.09516) | - | Jin et al. RL 训练 LLM 自主搜索 |
| 2025-03 | R1-Searcher: Incentivizing the Search Capability in LLMs via Reinforcement Learning | [Paper](https://arxiv.org/abs/2503.05592) | - | Song et al. 纯 RL 教会 LLM 自主调用搜索 |
| 2025-01 | Search-o1: Agentic Retrieval-Augmented Reasoning Models | [Paper](https://arxiv.org/abs/2501.05366) | - | Li et al. Agentic RAG 集成到推理模型，含 Reason-in-Documents 模块 |
| 2025-01 | CoRAG: Chain-of-Retrieval Augmented Generation | [Paper](https://arxiv.org/abs/2501.14342) | - | Wang et al. 训练模型生成中间检索链 |
| 2024-12 | GeAR: Graph Expansion Enhanced Retrieval | [Paper](https://arxiv.org/abs/2412.18431) | - | Shen et al. 图扩展增强检索器，处理多跳查询 |
| 2024-01 | Agent-G: Agentic Graph Retrieval Framework | [Paper](https://openreview.net/forum?id=g2C947jjjQ) | - | Lee et al. 基于代理的图检索框架，多代理动态分工 |

---

## GraphRAG (图 RAG)

通过构建知识图谱捕捉实体间的复杂关系，支持全局性问题回答。

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2025-02 | HippoRAG 2: From RAG to Human-Like Long-Term Memory | [Paper](https://arxiv.org/abs/2502.14802) | - | Gutierrez et al. 将 RAG 推向类人长期记忆系统 |
| 2024-04 | From Local to Global: A Graph RAG Approach to Query-Focused Summarization | [Paper](https://arxiv.org/abs/2404.16130) | [Code](https://github.com/microsoft/graphrag) | Edge et al. Microsoft. LLM 提取实体/关系 → 社区检测 → 分层摘要 → Map-Reduce 全局答案生成 |
| 2024-02 | G-Retriever: Retrieval-Augmented Generation for Textual Graph Understanding | [Paper](https://arxiv.org/abs/2402.07630) | - | He et al. 文本图理解与问答 |

---

## Multimodal RAG (多模态 RAG)

将 RAG 扩展到文本、图像、音频、视频等多种模态。

### Cross-Modal Retrieval (跨模态检索)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2024-11 | OmniSearch: Adaptive Multimodal Search | [Paper](https://arxiv.org/abs/2411.02937) | - | Li et al. 自适应多模态搜索 |
| 2024-07 | ColPali: Efficient Document Retrieval with Vision Language Models | [Paper](https://arxiv.org/abs/2407.01449) | - | Faysse et al. 视觉语言模型文档检索 |
| 2021-03 | CLIP: Learning Transferable Visual Models from Natural Language Supervision | [Paper](https://arxiv.org/abs/2103.00020) | [Code](https://github.com/openai/CLIP) | Radford et al. OpenAI. 图文跨模态对齐 |

### Frontier (前沿)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2025-12 | MegaRAG: Multimodal Knowledge Graph RAG | [Paper](https://arxiv.org/abs/2512.20626) | - | Hsiao et al. 多模态知识图谱 RAG |
| 2025-02 | ViDoRAG: Visual Document Retrieval with Multi-Agent RAG | [Paper](https://arxiv.org/abs/2502.18017) | - | Wang et al. 视觉文档多智能体 RAG，GMM 混合检索 + 迭代工作流 |
| 2024-11 | M3DocRAG: Multi-Modal Multi-Page Document RAG | [Paper](https://arxiv.org/abs/2411.04952) | - | Cho et al. 多页文档展平嵌入 |

---

## Evaluation (评估)

### Evaluation Frameworks (评估框架)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2025-01 | SafeRAG: Safety Benchmark for RAG | [Paper](https://arxiv.org/abs/2501.18636) | - | Liang et al. RAG 安全性基准 |
| 2024-04 | ClashEval: Knowledge Conflict Evaluation | [Paper](https://arxiv.org/abs/2404.10198) | - | Wu et al. 知识冲突评估 |
| 2024-01 | CRUD-RAG: Chinese RAG Benchmark | [Paper](https://arxiv.org/abs/2401.17043) | - | Lyu et al. 中文 RAG 基准 |
| 2023-11 | ARES: An Automated Evaluation Framework for RAG | [Paper](https://arxiv.org/abs/2311.09476) | - | Saad-Falcon et al. LLM 合成数据自动评估 |
| 2023-09 | RAGAS: Automated Evaluation of Retrieval Augmented Generation | [Paper](https://arxiv.org/abs/2309.15217) | [Code](https://github.com/explodinggradients/ragas) | Es et al. 自动化 RAG 评估框架 |
| 2023-09 | RGB: Benchmarking RAG with Noise, Negation, and Integration | [Paper](https://arxiv.org/abs/2309.01431) | - | Chen et al. 噪声、拒答与信息整合评测 |

### Benchmarks (通用基准)

| Date | Title | Paper | Code | Comment |
|------|-------|-------|------|---------|
| 2022-10 | MTEB: Massive Text Embedding Benchmark | [Paper](https://arxiv.org/abs/2210.07316) | [Code](https://github.com/embeddings-benchmark/mteb) | Muennighoff et al. 文本嵌入模型大规模基准 |
| 2021-04 | BEIR: A Heterogeneous Benchmark for Information Retrieval | [Paper](https://arxiv.org/abs/2104.08663) | - | Thakur et al. 零样本信息检索基准 |
| 2020-09 | KILT: Knowledge Intensive Language Tasks Benchmark | [Paper](https://arxiv.org/abs/2009.02252) | - | Petroni et al. 知识密集型任务基准 |

---

## Applications (应用)

| Domain | Date | Title | Paper | Code | Comment |
|--------|------|-------|-------|------|---------|
| Finance | 2024-03 | AlphaFin: Benchmarking Financial Analysis | [Paper](https://arxiv.org/abs/2403.12582) | - | Zhang et al. 金融分析基准 |
| Recommendation | 2024-03 | CoRAL: Collaborative Retrieval-Augmented LLMs for Recommendation | [Paper](https://arxiv.org/abs/2403.06447) | - | Wu et al. 协同检索增强推荐 |
| Medical | 2024-02 | REALM: Retrieval Augmented Large Medical Model | [Paper](https://arxiv.org/abs/2402.07016) | - | Zhu et al. 医疗领域检索增强 |
| Science | 2023-06 | MolReGPT: Molecular and Reaction Generative Pre-trained Transformer | [Paper](https://arxiv.org/abs/2306.06615) | - | Li et al. 分子科学 GPT |
| Legal | 2023-06 | ChatLaw: Open-Source Legal Large Language Model | [Paper](https://arxiv.org/abs/2306.16092) | [Code](https://github.com/PKU-YuanGroup/ChatLaw) | Cui et al. 开源法律大模型 |
| Dialogue | 2022-08 | BlenderBot 3: A Deployed Conversational Agent | [Paper](https://arxiv.org/abs/2208.03188) | [Code](https://github.com/facebookresearch/ParlAI) | Shuster et al. Meta 部署级对话代理 |
| Code | 2022-07 | DocPrompting: Generating Code by Retrieving the Docs | [Paper](https://arxiv.org/abs/2207.05987) | - | Zhou et al. 文档检索增强代码生成 |
| QA | 2017-04 | Reading Wikipedia to Answer Open-Domain Questions (DrQA) | [Paper](https://arxiv.org/abs/1704.00051) | [Code](https://github.com/facebookresearch/DrQA) | Chen et al. 开放域问答经典工作 |

---

## Contributing

欢迎贡献！请通过提交 Pull Request 或 Issue 来建议新的论文或资源。

### 快速贡献步骤

1. Fork 这个仓库
2. 创建你的特性分支 (`git checkout -b add-new-resource`)
3. 在表格中添加新资源（按时间倒序排列）
4. 提交你的改变 (`git commit -m 'Add: [Resource Title]'`)
5. 推送到分支 (`git push origin add-new-resource`)
6. 开启一个 Pull Request

### 表格字段说明

- **Date**: 论文发表日期 (YYYY-MM 格式，arXiv 论文以 arXiv ID 中的年月为准)
- **Title**: 论文标题
- **Paper**: 论文链接 (arXiv / 会议 / 博客)
- **Code**: 开源代码链接 (如无则留空 `-`)
- **Comment**: 简要描述主要贡献，包含作者、会议/期刊信息

---

## License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

本项目采用 [CC0 1.0 Universal License](LICENSE) 许可证。
