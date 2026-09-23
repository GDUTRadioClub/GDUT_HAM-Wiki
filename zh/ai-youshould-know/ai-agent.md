---
title: AI Agent：智能体
description: 能规划、调用工具并持续执行的 AI 系统
published: true
date: 2026-09-23T16:39:42.797Z
tags: 
editor: markdown
dateCreated: 2026-09-23T16:12:14.678Z
---

# AI Agent：智能体

> **一句话解释**：AI Agent 是能围绕目标进行规划、调用工具、观察结果并持续执行的 AI 系统。

---

## Agent 与聊天机器人的区别

普通聊天机器人：

```text
用户提问 → 模型回答 → 结束
```

AI Agent：

```text
目标 → 规划 → 调用工具 → 观察结果 → 调整计划 → 继续执行 → 完成目标
```

Agent 的关键不是“会说”，而是“会做”。

---

## Agent 的核心组成

| 组件 | 作用 |
|------|------|
| LLM | 理解目标、推理和决策 |
| Tools | 与外部世界交互的能力 |
| Memory | 记住历史与用户偏好 |
| Planning | 拆解任务、安排步骤 |
| Execution Loop | 执行、观察、反思、重试 |
| Guardrails | 权限控制与安全边界 |

---

## 常见 Agent 模式

- **ReAct**：推理 + 行动交替进行；
- **Plan-and-Execute**：先制定计划，再逐步执行；
- **Reflection**：执行后自我检查并改进；
- **Multi-Agent**：多个 Agent 分工协作。

---

## 应用场景

- 自动调研与报告生成；
- 代码修复与测试；
- 浏览器自动化；
- 客服与工单处理；
- 个人助理与工作流自动化。

---

## 延伸阅读

- [Tool Call：工具调用](/zh/ai-youshould-know/tool-call)
- [Skill：AI 技能](/zh/ai-youshould-know/skill)
- [MCP：模型上下文协议](/zh/ai-youshould-know/mcp)
- [AI时代你应该知道的-首页](/zh/ai-youshould-know)
