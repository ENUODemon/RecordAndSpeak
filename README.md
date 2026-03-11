# RecordAndSpeak

个人学习笔记与读书/技术笔记汇总仓库。

> 简短说明：本仓库用于记录个人在计算机、机器学习、数学、哲学、心理学、经济学、英语等领域的阅读笔记、面试题与学习资料，全部以 Markdown 文件组织，便于长期维护与检索。

最后更新：2026-03-11

## 项目概述

- **目的**：集中保存学习笔记、面试题与重要参考链接，作为个人复盘与长期知识库。
- **格式**：纯文本 Markdown（.md），图片或资源放在对应子目录下。

## 仓库结构（摘要）

- `ReadingNotes/`：主笔记目录，按主题分组。
	- `ReadingNotes/computer/`：前端、后端、面试题等（示例）。
	- `ReadingNotes/面试题/`：各类面试题与答案集合。
	- `ReadingNotes/MachineLearning/`：机器学习与深度学习相关笔记。
	- `ReadingNotes/Math/`：数学与统计学笔记。
	- `ReadingNotes/Philosophy/`：哲学类读书笔记。

你可以直接在仓库中浏览对应目录，或在本地使用编辑器打开查看（建议使用 VS Code、Obsidian、Typora 等）。

## 快速开始

克隆并打开仓库：

```bash
git clone https://github.com/enuodemon/RecordAndSpeak.git
cd RecordAndSpeak
code .
```

在 VS Code 中可以使用自带的 Markdown 预览（或安装 `Markdown All in One` 等扩展）来提高阅读体验。

## 使用建议

- 浏览：直接在 `ReadingNotes/` 目录下按主题打开对应 `.md` 文件。
- 搜索：使用编辑器全局搜索（或 ripgrep/`rg`）快速定位关键词。
- 编辑：新增笔记请放到合适的子目录，尽量保持文件名与主题相关，建议采用 `YYYY-MM-DD-简短标题.md` 或 `topic.md` 命名便于排序与查找。

每篇笔记建议包含：标题、时间、来源/参考（链接）、关键点与标签（Tag）。

## 贡献指南

欢迎 Fork 并提交改进。建议流程：

1. Fork 本仓库
2. 新建分支：`notes/<topic>-<brief>` 或 `feat/<something>`
3. 在对应目录添加或修改 `.md` 文件
4. 提交并通过 Pull Request 描述本次更改的目的与来源

在 PR 中请说明笔记来源（若摘自他人作品或课程），并确保保留必要的引用与链接。若要大规模转载或商业使用，请事先联系仓库所有者。

## 索引与改进建议（待办）

- 考虑添加一个顶层 `SUMMARY.md` 或自动化脚本，生成按主题的目录索引。
- 可以基于本仓库内容搭建静态站点（如 MkDocs、GitBook）以便阅读分享。

## 联系与许可

本仓库为个人学习笔记，版权归作者所有。如需使用、转载或合作，请通过提交 Issue 或 Pull Request 联系作者。

---

如果你希望我进一步：

- 我可以帮你生成 `SUMMARY.md` 索引并自动列出目录；
- 或者把笔记导出为 MkDocs / GitBook 的站点结构并写出配置示例。

请告诉我你想要的下一步。

