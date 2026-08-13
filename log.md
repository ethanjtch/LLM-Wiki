# 时间日志

append-only 操作记录。格式：`## [YYYY-MM-DD] 操作类型 | 标题`。

## [2026-08-12] setup | 初始化 LLM Wiki

按 Karpathy 的 LLM Wiki 模式初始化仓库：建立三层架构（`raw/` 原始来源层、`wiki/` wiki 层、`AGENTS.md` schema 层），创建 `index.md`、`log.md` 与 wiki 首页。

## [2026-08-12] ingest | 首批 6 篇文章

全部处理（全领域个人知识库定位）。来源页 6 篇，实体页 4（Netflix、Bela Bajaria、Ivan Zhao、Steph Ango），概念页 13（App与Web之争、封闭生态、截图传播、Agent、后视镜现象、思维自行车、水车效应、上下文碎片化、可验证性、奇迹材料、个人工单系统、工具敬畏、超服务受众），综合页 3（AI时代论与知识工作、技术变革的历史隐喻、平台与生态之争）。更新 index 与首页。

## [2026-08-12] lint | 首次健康检查

脚本比对 26 页链接图 + 抽查跨页事实一致性。结果：无红色链接、无孤儿页、数字一致、raw↔sources 一一对应。修复 3 处：平台与生态之争 `sources` 2→3、工具敬畏补 [[超服务受众]] 反向链接、首页 [[index]]/[[log]] 格式统一。落盘综合页《知识库健康检查（2026-08）》，提出待建概念页 4（MCP/WebMCP、红旗法案、共同许可、熟食店汉堡标准）与新来源建议 3 条。

## [2026-08-13] ingest | Anthropic 长期运行 Agent 工程（2 篇）

处理 raw/ 新导入的 2 篇 Anthropic 工程博客（《Effective harnesses for long-running agents》2025-11、《Harness design for long-running application development》2026-05）。来源页 2，概念页 5（harness（代理框架）、上下文焦虑、上下文重置、自我评估偏差、生成器评估器循环），实体页 1（Anthropic），综合页 1（长期运行代理的工程实践）。更新 Agent/可验证性/上下文碎片化/AI时代论与知识工作 4 页——特别是为[[可验证性]]的未决问题补上工程化答案雏形（评分标准改写 + 独立评审 + 浏览器自动化点测）。更新 index 与首页。

