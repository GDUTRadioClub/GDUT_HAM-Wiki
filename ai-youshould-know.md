---
title: AI时代你应该知道的-首页
description: AI 名词速查与入门索引：KVCache、LLM 推理、MCP、Skill、Tool Call 等
published: true
date: 2026-09-23T16:08:44.015Z
tags: 
editor: markdown
dateCreated: 2026-09-23T15:51:58.268Z
---

# AI时代你应该知道的-首页

> 一份写给开发者与普通用户的 **AI 名词速查与入门索引**。
>
> 这里不追求堆砌公式，而是先用一句话讲清楚“它是什么、解决什么问题、和哪些概念相关”，再通过链接进入对应详情页。

---

## 📚 快速索引

| 名词 | 一句话解释 | 详情 |
|------|-----------|------|
| **LLM** | 大语言模型，通过海量文本训练、能够生成与理解自然语言的神经网络 | 本文 |
| **Token** | 模型处理文本的最小单位，可以粗略理解为“词元/字块” | 本文 |
| **Prompt** | 用户给模型的输入指令或上下文，决定输出方向 | 本文 |
| **Context Window** | 模型一次能“看见”的最大 Token 数量，超出会被截断或需要压缩 | 本文 |
| **LLM 推理** | 模型根据输入逐步生成输出的过程，分为 Prefill 与 Decode 两个阶段 | [查看详情](/en/ai-youshould-know/llm-inference) |
| **KVCache** | 缓存 Attention 中的 Key/Value，避免 Decode 阶段重复计算，显著加速生成 | [查看详情](/en/ai-youshould-know/kvcache) |
| **MCP** | Model Context Protocol，让模型/Agent 用统一协议连接外部工具与数据源 | [查看详情](/en/ai-youshould-know/mcp) |
| **Skill** | 可复用的能力包，把提示词、工具调用流程和领域知识封装成“技能” | [查看详情](/en/ai-youshould-know/skill) |
| **Tool Call** | 模型按约定格式请求调用外部函数/API，并把结果继续用于推理 | [查看详情](/en/ai-youshould-know/tool-call) |
| **RAG** | 检索增强生成：先查资料，再让模型基于资料回答 | [查看详情](/en/ai-youshould-know/rag) |
| **AI Agent** | 能感知目标、规划步骤、调用工具并根据反馈持续执行的 AI 系统 | [查看详情](/en/ai-youshould-know/ai-agent) |
| **Token 与上下文窗口** | Token 与上下文长度的工程影响 | [查看详情](/en/ai-youshould-know/token-and-context) |
| **Fine-tuning** | 在预训练模型基础上，用特定数据继续训练以适配任务 | 本文 |
| **LoRA** | 低秩适配，用少量参数完成高效微调 | 本文 |
| **Quantization** | 量化，把模型权重/激活从高精度压缩到低精度，降低显存与成本 | 本文 |
| **RLHF** | 基于人类反馈的强化学习，让模型输出更符合人类偏好 | 本文 |
| **MoE** | 混合专家模型，每次只激活部分专家，兼顾规模与推理成本 | 本文 |
| **Multimodal** | 多模态，模型同时处理文本、图片、音频、视频等信息 | 本文 |
| **Hallucination** | 幻觉，模型生成看似合理但实际错误或不存在的内容 | 本文 |
| **Prompt Injection** | 提示词注入，攻击者通过输入诱导模型忽略原有指令或泄露信息 | 本文 |
| **Alignment** | 对齐，让 AI 的目标、行为与人类价值观和安全要求保持一致 | 本文 |

---

## 🧱 基础概念

### LLM（大语言模型）
LLM 是 **Large Language Model** 的缩写。它基于 Transformer 架构，通过大规模文本预训练学习语言规律，并具备生成、总结、翻译、推理、代码等能力。

### Token（词元）
Token 是模型处理文本的基本单位。英文里一个单词可能被拆成多个 Token，中文通常一个字或几个字一个 Token。模型的上下文长度、计费、推理速度都和 Token 数量直接相关。

### Prompt（提示词）
Prompt 是输入给模型的全部内容，包括系统指令、用户问题、上下文和示例。Prompt 的设计质量会显著影响输出效果。

### Context Window（上下文窗口）
Context Window 是模型单次请求能容纳的最大 Token 数。窗口越大，模型能参考的资料越多，但显存占用、延迟和成本也越高。

### Embedding（向量化）
Embedding 把文本、图片等内容映射为高维向量，使语义相近的内容在向量空间中距离更近。它是语义搜索、RAG、推荐和聚类的基础。

### Transformer 与 Attention（注意力机制）
Transformer 是目前主流大模型的骨架。Attention 让模型在处理某个 Token 时，能够关注序列中其他相关 Token，从而理解上下文关系。

### 多模态（Multimodal）
多模态模型可以同时理解和生成文本、图像、音频、视频等内容。例如把图片作为输入进行问答，或根据文字生成图片。

### 幻觉（Hallucination）
幻觉指模型生成了流畅但错误、过时或虚构的信息。RAG、工具调用、引用来源和事实校验都能降低幻觉风险。

---

## ⚡ 推理与性能

### LLM 推理（LLM Inference）
推理是模型根据输入生成输出的过程。它通常分为两个阶段：
- **Prefill**：并行处理输入 Prompt，建立 KVCache；
- **Decode**：逐个 Token 自回归生成，直到结束。

推理优化关注首 Token 延迟、每 Token 延迟、吞吐量和显存占用。

### KVCache
KVCache 缓存每一层 Attention 的 Key/Value 张量，使 Decode 阶段不必重复计算历史 Token。它是 LLM 推理加速的核心机制之一，也是长上下文显存占用的主要来源。

### Prefill / Decode
Prefill 阶段计算密集，Decode 阶段更受显存带宽限制。理解这两个阶段，有助于选择合适的批处理、量化和缓存策略。

### Quantization（量化）
量化把 FP16/BF16 权重或激活压缩为 INT8、INT4 等低精度格式，从而降低显存占用、提升推理速度，但可能带来精度损失。

### Continuous Batching（连续批处理）
把不同请求动态拼接进同一批次，在请求结束时立即插入新请求，从而提升 GPU 利用率和吞吐量。

### Speculative Decoding（投机解码）
用一个小模型快速草拟多个 Token，再由大模型并行验证，在保持输出质量的同时加速生成。

### MoE（混合专家）
MoE 模型包含多个“专家”子网络，每次只激活其中少数专家。它让模型参数量很大，但单次推理计算量相对可控。

---

## 🎯 Agent、工具与协议

### AI Agent（智能体）
Agent 不只是回答问题，而是围绕目标进行规划、调用工具、观察结果、修正计划并继续执行。它通常由大模型、工具、记忆和执行循环组成。

### Tool Call / Function Calling（工具调用）
Tool Call 让模型输出结构化的函数调用请求，由外部系统执行后再把结果返回给模型。它让 AI 能查数据库、发邮件、操作浏览器、调用业务 API。

### MCP
MCP（Model Context Protocol）是一个开放协议，用统一方式把模型或 Agent 连接到外部工具、资源和提示词。可以把它理解为“AI 世界的 USB-C 接口”。

### Skill（技能）
Skill 是可复用的能力封装，通常包括提示词、工具调用流程、领域知识和输出规范。它让 Agent 不必每次从零开始解决同类任务。

### RAG（检索增强生成）
RAG 先从知识库检索相关片段，再把片段作为上下文交给模型生成回答。它适合企业知识库、文档问答和需要引用来源的场景。

### Memory（记忆）
Memory 让 Agent 跨会话记住用户偏好、项目状态或历史结论。常见形式包括短期上下文、长期向量记忆和结构化数据库。

### Planning（规划）
Planning 指模型把复杂目标拆解为可执行步骤，并根据中间结果动态调整。它是 Agent 从“聊天”走向“做事”的关键。

---

## 🛠️ 训练、适配与安全

### Fine-tuning（微调）
在预训练模型基础上，用特定领域数据继续训练，使模型更适配某个任务或风格。

### LoRA
LoRA 通过训练少量低秩矩阵来近似全量微调，大幅降低显存和存储成本，适合快速定制模型。

### RLHF
RLHF 使用人类偏好数据训练奖励模型，再通过强化学习优化语言模型，使其输出更有帮助、更诚实、更安全。

### Alignment（对齐）
对齐关注如何让 AI 系统理解并遵循人类意图、价值观和安全边界，是 AI 安全的核心议题。

### Prompt Injection（提示词注入）
攻击者把恶意指令混入文档、网页或用户输入中，诱导模型泄露信息或执行非预期操作。防护手段包括权限隔离、输入过滤和工具最小权限。

### Guardrails（护栏）
护栏是围绕模型输入、输出和工具调用设置的安全与合规规则，用于阻止有害内容、数据泄露和越权操作。

### Evaluation（评估）
评估用基准测试、人工评分和线上指标衡量模型或 Agent 的质量。常见维度包括准确性、安全性、延迟、成本和稳定性。

---

## 🧭 如何阅读这个 Wiki

- 想了解 **模型为什么快/慢**：从 [LLM 推理](/en/ai-youshould-know/llm-inference) 和 [KVCache](/en/ai-youshould-know/kvcache) 开始。
- 想了解 **Agent 怎么调用外部能力**：从 [Tool Call](/en/ai-youshould-know/tool-call)、[MCP](/en/ai-youshould-know/mcp) 和 [Skill](/en/ai-youshould-know/skill) 开始。
- 想了解 **企业知识库问答**：重点关注 [RAG](/en/ai-youshould-know/rag)、Embedding、Memory 和 Evaluation。

> 📌 本页会持续更新。欢迎补充你遇到的 AI 新名词、使用经验和踩坑记录。
