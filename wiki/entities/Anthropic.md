---
title: Anthropic
type: entity
tags:
  - 组织
  - AI
  - Agent
created: 2026-08-13
updated: 2026-08-13
sources: 2
---

## 定义
AI 安全与研究的公司（Claude 系列模型、Claude Agent SDK、Claude Code 的开发者）。对本 wiki 的意义：它是**长期运行 Agent 工程方法论**的主要公开来源，持续产出关于 harness 设计、上下文工程、代理最佳实践的一手经验。

## 关键事实
- **定位**：自称 "AI safety and research company"，目标是构建"可靠、可解释、可操控"的 AI 系统；设 Anthropic Labs 做前沿实验（[[长期运行应用开发的框架设计（Anthropic）]] 出自其成员）。
- **方法论输出**：
  - *Effective harnesses for long-running agents*（2025-11，Justin Young）：初始化代理 + 编码代理，验证"跨上下文窗口渐进推进"的可行性；
  - *Harness design for long-running application development*（2026-05，Prithvi Rajasekaran）：GAN 启发式三代理（planner/generator/evaluator），从"跨会话编码"升级到"数小时自主构建全栈应用"；
  - 关联工作：前端设计 skill、context engineering 博客、*Building Effective Agents*（"先最简单，需要再加复杂度"原则）。
- **实证风格**：公开博客带真实成本/时长/失败报告（如 solo vs harness 对比：$9/20min vs $200/6hr），并坦白评估器被调教前的缺陷。
- **对 AGENTS.md 的呼应**：本仓库即复用其"progress 文件 + git + 结构化工件交接"模式的一部分（LLM Wiki 的 `log.md`）。

## 相关来源
- [[长期运行代理的有效管理工具（Anthropic）]]
- [[长期运行应用开发的框架设计（Anthropic）]]

## 相关页面
- [[harness（代理框架）]]、[[生成器评估器循环]]、[[上下文重置]]、[[长期运行代理的工程实践]]、[[Agent]]