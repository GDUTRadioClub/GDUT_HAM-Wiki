---
title: LLM 推理：从输入到输出
description: Prefill、Decode、采样策略与推理优化
published: true
date: 2026-09-23T16:11:24.346Z
tags: 
editor: markdown
dateCreated: 2026-09-23T16:11:24.346Z
---

# LLM 推理：从输入到输出

> **一句话解释**：LLM 推理是模型根据输入逐步生成输出的过程，通常分为 Prefill 和 Decode 两个阶段。

---

## 什么是推理？

训练是让模型学习参数；推理是使用已经训练好的模型完成实际任务。

用户输入一段 Prompt，模型输出一段文本，这个过程就是推理。

在工程上，推理关注的不只是“答得对不对”，还包括：

- **首 Token 延迟（TTFT）**：用户等多久看到第一个字；
- **每 Token 延迟（TPOT）**：后续文字生成得有多快；
- **吞吐量（Throughput）**：单位时间能服务多少请求；
- **显存占用**：能同时承载多长上下文、多少并发；
- **成本**：每百万 Token 的 GPU 费用。

---

## 两个关键阶段

### 1. Prefill（预填充）
模型一次性处理整段输入 Prompt，计算所有 Token 的 Attention 和中间状态。

特点：
- 计算密集；
- 可并行处理；
- 会建立 [KVCache](/en/ai-youshould-know/kvcache)；
- 直接影响首 Token 延迟。

### 2. Decode（解码）
模型基于已有上下文，逐个 Token 自回归生成输出。

特点：
- 每步只生成一个 Token；
- 需要反复读取 KVCache；
- 更受显存带宽限制；
- 决定输出速度和吞吐量。

---

## 采样与生成策略

模型输出的是下一个 Token 的概率分布。如何从分布中选 Token，就是采样策略：

- **Greedy**：每次选概率最大的 Token，稳定但可能重复；
- **Temperature**：温度越高越随机，越低越确定；
- **Top-k**：只从概率最高的 k 个 Token 中采样；
- **Top-p / Nucleus**：从累计概率达到 p 的最小集合中采样；
- **Repetition Penalty**：降低重复 Token 的概率。

---

## 常见推理优化

| 优化 | 作用 |
|------|------|
| KVCache | 避免重复计算历史 Token |
| 量化 | 降低权重/激活精度，减少显存 |
| Continuous Batching | 动态拼批，提升 GPU 利用率 |
| PagedAttention | 分页管理 KVCache，减少碎片 |
| Speculative Decoding | 小模型草拟 + 大模型验证，加速生成 |
| Prefix Caching | 复用公共前缀的 KVCache |
| MoE | 每次只激活部分专家，降低计算量 |

---

## 推理框架

常见推理与服务框架包括：

- **vLLM**：高吞吐、PagedAttention、Continuous Batching；
- **TensorRT-LLM**：NVIDIA 生态，面向极致性能；
- **SGLang**：面向结构化生成和 Agent 场景；
- **llama.cpp / Ollama**：本地 CPU/GPU 推理；
- **Hugging Face TGI**：生产级文本生成推理服务。

---

## 延伸阅读

- [KVCache：键值缓存](/en/ai-youshould-know/kvcache)
- [AI时代你应该知道的-首页](/en/ai-youshould-know)
