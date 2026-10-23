# `cards/` · 每张卡一个目录

## 目录命名

`<feat|fix>-<卡号>-<slug>/`，例如 `feat-<卡号>-task-status-filter/`、`fix-<卡号>-archived-task-reminders/`。以下 `DEMO-*` 卡号、日期与代码名均为虚构示例，真实卡使用用户提供的标识与实际日期。

- 卡号来自用户（BA 的卡片工具），AI 不自编。卡号格式以团队卡片工具为准（落地时从 git log 或 BA 处确认，写在这里）。
- slug：3–5 个英文单词，kebab-case，取自卡标题。
- 以 `_` 开头的目录是示例或模板，不是真实卡。

## 目录内文件

| 文件 | 阶段 | 模板 |
|---|---|---|
| `README.md` | 01 建立，全程更新 `stage` | 见下 |
| `01-card.md` | 01 读卡 | `templates/card-analysis.md` 第一部分 |
| `02-questions.md` | 02 拆问题 | `templates/card-analysis.md` 第二、三部分 |
| `03-alignment.md` | 03 对齐 | `templates/alignment.md` |
| `04-dev-plan.md` | 04 制定开发计划 | `templates/dev-plan.md` |
| `tasks/T<nn>-<slug>.md` | 04 拆解产出，05 执行与评审 | `templates/subtask.md` |
| `05-dev-log.md` | 05 开发（协调窗口维护） | `templates/dev-log.md` |
| `05-card-review.md` | 05 卡级代码评审（推送前） | `templates/card-review.md` |
| `06-desk-check.md` | 06 DC、07 回填 | `templates/desk-check.md` |
| `context-notes.md` | 任意阶段，可选 | 自由格式：来源、事实、对本卡的影响 |
| `research/<topic>.md` | 任意阶段，可选 | 一题一文件；外部资料要带来源与原文片段 |
| `assets/` | 任意阶段，可选 | 截图、样例请求 |
| `handoff-<日期>.md` | 阶段中途换窗口，可选 | 见 `workflow/session-protocol.md` |

## `README.md` frontmatter

```yaml
---
id: DEMO-123
type: feat            # feat | fix
title: 任务列表按状态筛选
stage: intake         # intake | clarifying | aligning | planning | ready-for-dev | in-dev | desk-check | in-qa | done
primary_repo: <主仓库名>
linked_repo: <对端仓库名>   # 无则删掉此行
created: 2026-09-21
links:
  - 原卡：<URL 或"BA 手动粘贴">
  - 关联卡：fix-DEMO-130-...（如有）
---
```

frontmatter 下面只写一段话：这张卡现在到哪一步、下一步是什么。过程历史（每轮澄清、每次评审、每次偏差）写进 02/03/05 与 `journal/`，不在本文件堆叠。

澄清与对齐可以多轮往返：交互进行中、草稿待 Dev 审阅或需展开下一轮时为 `clarifying`；本轮问卷已审阅并等待答复，或已收到答复正在整理对齐文档、等待批准时为 `aligning`。`align` 启动后在这两个状态间自动继续设计树追问与回填，无需用户切换命令。每轮记录并呈现依赖展开、场景与冲突、AC 覆盖及本轮判断的依据，Q 编号保留、新题递增，原答复与修订依据不覆盖。只有 03 的收敛门禁通过并获明确批准，才能进入 `planning`；具体命令与回流按 `workflow/overview.md`、`workflow/session-protocol.md`。

## 主仓库与链接仓库

- 一张卡的文档只存一份，放**主改动仓库**（改动多的一方，通常是后端）。
- 另一仓库建同名目录，只放一个 `README.md`：

```markdown
---
id: DEMO-123
type: feat
stage: in-dev
primary_repo: <主仓库名>
---
本卡文档在 `<主仓库名>/.ai/cards/feat-DEMO-123-task-status-filter/`。
本仓库改动摘要（虚构示例）：`TaskListPage.tsx` 增加状态筛选项；`types/index.ts` 的 `TaskQueryParams` 增加 `status`。
```

## 归档

`stage: done` 后把目录移到 `archive/YYYY-MM/`（按结卡月份）。链接仓库的同名目录一并移动。归档卡是历史卡查询的来源（读卡阶段会翻）。

## 示例

接入时可在目标项目内编写 `_example-feat-0000-sample/` 作为格式样板；模板包不包含真实业务卡。对外分享样板时使用虚构模块与数据，不把内部需求或证据一起发布。
