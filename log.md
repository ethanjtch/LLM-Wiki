---
title: 时间日志
type: log
---

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

## [2026-08-13] lint | 二次健康检查（含系统层部署体检）

内容层：脚本扫描 37 个 wiki 页 + index.md 链接图，无红色链接、无孤儿页、无 index↔页面不一致、无矛盾。23 页 updated 停在 08-12 属未改动豁免。系统层：git 与 origin 同步、Actions 3 次连续 success、站点关键页面全 200、wikilink 跳转正常。沉淀综合页[[知识库健康检查（2026-08-13二次）]]。附：构建管道三坑（symlink 无限递归、软链目标目录名污染 URL、KaTeX 对中文 $ 误报）已修复，均见 deploy.yml/quartz.config.yaml 与 log 相关条目。

## [2026-08-13] setup | 站点首页改造 + 菜单栏链接修复

改造（只动 CI 与 publish/，wiki 文档一字未改）：① `wiki/首页.md` 设为站点首页 → 访问根路径 `/` 即渲染「LLM Wiki 首页」门面页，原目录页 `index.md` 于构建时改名 `索引` 保留，全库 `[[index]]` 链接在 CI 中重写为 `[[索引]]`（sed 替 heredoc、python 单行遍历）；② 修复菜单栏/search 跳转丢 `/LLM-Wiki` 前缀：`quartz.config.yaml` `baseUrl` 由 `ethanjtch.github.io` 改为 `ethanjtch.github.io/LLM-Wiki`，线上 `<body data-basepath="/LLM-Wiki">` 生效。验证：线上 `/`、`/索引` 200，search/explorer 链接正确；本地 Quartz serve（/tmp/quartz-local）复现一致性。

## [2026-08-13] setup | 绑定自定义域名 wiki.ethanfun.xyz

Cloudflare DNS（CNAME wiki → ethanjtch.github.io，手动配置）已验证生效。`quartz.config.yaml` `baseUrl` 改为 `wiki.ethanfun.xyz`，CNAME 插件自动生成 CNAME 文件随部署上线，GitHub Pages 设置自定义域名并签发 Let's Encrypt 证书。验证：`https://wiki.ethanfun.xyz/` 200、`/索引` 200、HTTPS 强制可用；旧地址 `ethanjtch.github.io/LLM-Wiki` 因自定义域名自动 404。

## [2026-08-13] setup | 添加站点图标与版权声明

favicon：用户从 [Flaticon Wikipedia icons](https://www.flaticon.com/free-icons/wikipedia) 下载 Magnific 的 Wikipedia 图标（512×512 PNG）存入 `publish/assets/wikipedia.png`，CI 构建时复制为引擎 `quartz/static/icon.png`，favicon 插件生成 48×48 favicon.ico。footer：`links` 增加版权行「Icons by Magnific (Flaticon)」链接回 Flaticon 授权页。验证：线上 `/favicon.ico` 200、footer 链接正常。

