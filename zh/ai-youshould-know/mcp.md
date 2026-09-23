---
title: MCP：模型上下文协议
description: 用统一协议连接模型、Agent 与外部工具和数据源
published: true
date: 2026-09-23T16:11:33.334Z
tags: 
editor: markdown
dateCreated: 2026-09-23T16:11:33.334Z
---

# MCP：模型上下文协议

> **一句话解释**：MCP（Model Context Protocol）是一个开放协议，用统一方式把模型或 Agent 连接到外部工具、数据源和提示词。

---

## MCP 解决什么问题？

在 MCP 出现之前，每个 AI 应用都要为不同的工具、数据库、SaaS 服务写一套专用集成：

- 接 GitHub 一套代码；
- 接数据库一套代码；
- 接内部知识库又一套代码；
- 换个模型或 Agent 框架还要重写。

MCP 的目标是提供一层 **标准接口**，让“模型/Agent”和“外部能力”解耦。

可以把它类比为：

- USB-C 统一了设备接口；
- HTTP 统一了 Web 通信；
- MCP 希望统一 AI 与工具/数据之间的连接方式。

---

## 核心角色

MCP 采用客户端 / 服务器架构：

| 角色 | 作用 |
|------|------|
| **MCP Host** | 运行 AI 应用或 Agent 的宿主，例如 IDE、聊天客户端、Agent 平台 |
| **MCP Client** | Host 内部负责与 MCP Server 建立连接、发送请求的组件 |
| **MCP Server** | 对外暴露工具、资源、提示词等能力的服务 |

一个 Host 可以同时连接多个 MCP Server。

---

## MCP Server 能提供什么？

MCP 常见能力包括：

- **Tools（工具）**：可被模型调用的函数，例如查询天气、执行 SQL、发送消息；
- **Resources（资源）**：可读取的数据，例如文件、数据库记录、网页内容；
- **Prompts（提示词模板）**：预定义的提示词或工作流模板；
- **Sampling**：Server 可以请求 Host 侧的模型进行生成。

---

## MCP 与 Tool Call 的关系

- **Tool Call** 更偏向模型与推理 API 之间的“函数调用”机制；
- **MCP** 更偏向工具与数据源的标准化接入协议；
- MCP Server 暴露的 Tools，最终往往通过 Tool Call 被模型调用。

两者不是替代关系，而是不同层次：

```text
用户 → Agent → Tool Call → MCP Client → MCP Server → 外部系统
```

---

## 典型使用场景

- 让 AI IDE 读取项目文件、Git 历史、数据库结构；
- 让企业 Agent 连接内部知识库、工单系统、CRM；
- 让个人助理统一接入日历、邮件、笔记和浏览器；
- 让不同模型厂商的客户端复用同一批工具生态。

---

## 安全注意事项

MCP 让 AI 获得真实世界操作能力，因此必须关注：

- **最小权限**：只暴露必要的工具和字段；
- **身份认证**：Server 需要验证调用方身份；
- **审计日志**：记录谁在何时调用了什么工具；
- **提示词注入**：外部数据可能诱导模型越权；
- **人工确认**：高风险操作应要求用户确认。

---

## 延伸阅读

- [Tool Call：工具调用](/en/ai-youshould-know/tool-call)
- [Skill：AI 技能](/en/ai-youshould-know/skill)
- [AI时代你应该知道的-首页](/en/ai-youshould-know)
