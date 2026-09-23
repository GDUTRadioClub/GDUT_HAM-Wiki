---
title: Token 与上下文窗口
description: 模型处理文本的最小单位与上下文长度限制
published: true
date: 2026-09-23T16:39:45.139Z
tags: 
editor: markdown
dateCreated: 2026-09-23T16:12:23.660Z
---

# Token 与上下文窗口

> **一句话解释**：Token 是模型处理文本的最小单位；上下文窗口是模型一次能处理的 Token 上限。

---

## Token 是什么？

模型不直接读“字”或“单词”，而是先把文本切分成 Token。

例如：

- 英文 `unbelievable` 可能被拆成 `un` + `believ` + `able`；
- 中文可能一个字一个 Token，也可能多个字组成一个 Token。

Token 数量影响：

- 上下文长度；
- API 计费；
- 推理速度；
- 显存占用。

---

## 上下文窗口

上下文窗口（Context Window）是模型单次请求能容纳的最大 Token 数，包括：

- 系统提示词；
- 历史对话；
- 用户当前问题；
- 检索到的资料；
- 模型即将生成的输出。

如果超出窗口，就需要截断、摘要或使用 RAG 压缩上下文。

---

## 为什么大窗口不等于无限记忆？

- 窗口越大，KVCache 显存占用越高；
- 长上下文中的信息可能被“稀释”；
- 模型仍可能忽略中间内容；
- 成本随 Token 数增加。

因此，**会检索、会压缩、会遗忘** 比单纯追求大窗口更重要。

---

## 延伸阅读

- [KVCache：键值缓存](/zh/ai-youshould-know/kvcache)
- [LLM 推理：从输入到输出](/zh/ai-youshould-know/llm-inference)
- [AI时代你应该知道的-首页](/zh/ai-youshould-know)
