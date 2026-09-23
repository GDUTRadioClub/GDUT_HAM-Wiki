---
title: KVCache：键值缓存
description: LLM 推理加速的核心：KVCache 原理、内存成本与优化方向
published: true
date: 2026-09-23T16:39:30.447Z
tags: 
editor: markdown
dateCreated: 2026-09-23T16:10:58.911Z
---

# KVCache：键值缓存

> **一句话解释**：KVCache 缓存 Attention 中的 Key/Value 张量，让 Decode 阶段不必重复计算历史 Token，是 LLM 推理加速的核心机制之一。

---

## 为什么需要 KVCache？

LLM 生成文本时是 **自回归** 的：每生成一个 Token，都要把它加入上下文，再预测下一个 Token。

如果每一步都对全部历史 Token 重新计算 Attention，那么生成长文本的计算量会随长度快速增长，延迟和成本都不可接受。

KVCache 的做法是：

- 在 **Prefill 阶段** 一次性计算输入 Prompt 的每层 Key/Value，并缓存起来；
- 在 **Decode 阶段** 每生成一个新 Token，只计算这个新 Token 的 Query/Key/Value；
- 把新的 Key/Value 追加到缓存中，Attention 直接复用历史缓存。

这样，每个新 Token 的 Attention 计算量大致只与当前上下文长度线性相关，而不是每步都从头平方级重算。

---

## Prefill 与 Decode 的差异

| 阶段 | 特点 | 是否使用 KVCache |
|------|------|------------------|
| Prefill | 一次处理整段 Prompt，计算密集，可并行 | 建立 KVCache |
| Decode | 逐个 Token 生成，受显存带宽限制 | 读取并追加 KVCache |

因此，KVCache 对 Decode 阶段尤其关键。

---

## KVCache 的内存成本

KVCache 大小大致与以下因素成正比：

- 层数
- 注意力头数
- 头维度
- 序列长度
- 批大小
- 数据类型（FP16 / INT8 / INT4）

上下文越长、并发越高，KVCache 占用越明显。长上下文推理中，它经常是显存瓶颈。

---

## 常见优化方向

### 1. 减少缓存精度
把 KVCache 从 FP16 量化为 INT8/INT4，降低显存占用。

### 2. 共享 KV 头
使用 MQA（Multi-Query Attention）或 GQA（Grouped-Query Attention），让多个 Query 头共享更少的 Key/Value 头。

### 3. 分页管理
PagedAttention 把 KVCache 分成固定大小的块，像操作系统管理内存一样按需分配，减少碎片、提升并发。

### 4. 滑动窗口 / 稀疏注意力
只保留最近一段窗口，或只保留重要 Token，控制缓存长度。

### 5. 前缀缓存
多个请求共享相同系统提示词时，可以复用相同前缀的 KVCache。

---

## 和 LLM 推理的关系

KVCache 是 [LLM 推理](/zh/ai-youshould-know/llm-inference) 中 Prefill/Decode 两阶段设计的核心产物：

- 没有 KVCache，Decode 会非常慢；
- 有了 KVCache，显存管理成为新的工程重点；
- 很多推理框架（如 vLLM、TensorRT-LLM、SGLang）都在 KVCache 管理上做优化。

---

## 延伸阅读

- [LLM 推理：从输入到输出](/zh/ai-youshould-know/llm-inference)
- [AI时代你应该知道的-首页](/zh/ai-youshould-know)
