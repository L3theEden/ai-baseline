# `cards/` · 每张卡一个目录

## 目录命名

`<feat|fix>-<卡号>-<slug>/`，例如 `feat-<卡号>-task-status-filter/`、`fix-<卡号>-archived-task-reminders/`。以下 `DEMO-*` 卡号、日期与代码名均为虚构示例，真实卡使用用户提供的标识与实际日期。

- 完整流程卡号来自用户的卡片工具，AI 不自编外部编号；格式按团队约定。轻量维护无外部编号时可按 [维护协议](../workflow/maintenance.md#记录状态与授权) 使用明确标记的本地维护标识；升级完整时保留该标识，取得外部编号后补关联。
- slug：3–5 个英文单词，kebab-case，取自卡标题。
- 以 `_` 开头的目录是示例或模板，不是真实卡。

## 目录内文件

完整流程按阶段生成下表文件；轻量维护只需要 `README.md` 与 `maintenance.md`（模板 `templates/maintenance.md`），证据按需附加。不要为轻量维护预建完整阶段空文件。

| 文件 | 阶段 | 模板 |
|---|---|---|
| `README.md` | 01 建立，全程更新 `stage` | 见下 |
| `01-card.md` | 01 读卡 | `templates/card-analysis.md` 第一部分 |
| `02-questions.md` | 02 与 Dev 澄清 | `templates/card-analysis.md` 第二部分；价值疑点按需用第三部分 |
| `03-alignment.md` | 03 对齐 | `templates/alignment.md` |
| `04-dev-plan.md` | 04 制定开发计划 | `templates/dev-plan.md` |
| `tasks/T<nn>-<slug>.md` | 04 拆解产出，05 执行与评审 | `templates/subtask.md` |
| `05-dev-log.md` | 05 开发（协调窗口维护） | `templates/dev-log.md` |
| `05-card-review.md` | 05 卡级代码评审（推送前） | `templates/card-review.md` |
| `06-desk-check.md` | 06 DC、07 回填 | `templates/desk-check.md` |
| `context-notes.md` | 任意阶段，可选 | 自由格式：来源、事实、对本卡的影响 |
| `research/<topic>.md` | 任意阶段，可选 | 一题一文件；外部资料要带来源与原文片段 |
| `assets/` | 任意阶段，可选 | 截图、样例请求 |
| `handoff-<日期>-<序号>.md` | 阶段中途换窗口，可选；同日递增 | 见 `workflow/session-protocol.md`；旧文件名可保留 |

## `README.md` frontmatter

```yaml
---
id: DEMO-123
type: feat            # feat | fix
title: 任务列表按状态筛选
workflow: full        # full | maintenance；旧卡缺省 full
stage: intake         # intake | clarifying | aligning | planning | ready-for-dev | in-dev | desk-check | in-qa | done
primary_repo: <主仓库名>
linked_repo: <对端仓库名>   # 无则删掉此行
created: 2026-09-21
links:
  - 原卡：<URL 或"BA 手动粘贴">
  - 关联卡：fix-DEMO-130-...（如有）
---
```

`workflow` 只决定使用哪条流程，`stage` 是进度唯一来源。轻量维护使用 `type: fix`、`workflow: maintenance`，阶段仅为 `intake / in-dev / done`，其他字段与恢复摘要沿用；升级完整按维护协议改字段并保留历史，不改旧卡的批准或状态来代替本次记录。

## 当前恢复摘要

frontmatter 下保留下面四项，简短到新会话能直接定位下一步；`stage` 只以 frontmatter 为准，不再维护一份阶段表。更新摘要时替换旧摘要，过程历史保存在阶段产物中。

- **有效产物**：<本阶段适用的文件 / 章节、版本或期号、批准状态及批准记录指针；尚未形成写“未产出”，未知版本写“未登记”，不补造批准>。
- **当前阻塞**：<问题 / 子任务的编号与来源指针，以及解除条件；没有写“无”>。
- **下一步**：<当前允许的具体动作、由谁处理；换窗口时附相应阶段命令>。
- **恢复阅读**：<当前阶段必要的文件 / 章节，若有有效交接则只链接当前交接文件>。

摘要只作导航，不能代替完整流程 03/04 的批准、子任务状态、轻量维护的实现授权或评审结果。恢复时核对被引用的正文；发现矛盾按 [会话协议](../workflow/session-protocol.md#开场每个窗口都做) 查证，不因摘要较新就忽略已有门禁。

**历史整理：** 每轮澄清、答复、批准、评审和偏差保留在 02/03/04/05 或 `maintenance.md` 等对应产物。旧 README 中的独有记录先移入对应阶段记录或 `research/history/` 并留指针，再收短入口，不能直接删掉依据。旧交接记录保留，更新时注明被哪份记录或阶段产物取代；同日另建递增序号文件，不覆盖原文。移动或归档后核对现行引用，详见 [文档检查](../workflow/documentation.md#文档检查)。

完整流程的澄清与对齐可多轮往返：与 Dev 讨论、查证、审阅业务问题草稿或展开关键分支时为 `clarifying`；澄清已收敛、准备或正在整理共识，或等待已审阅的 BA 问题答复且当前无可继续的 Dev 讨论，或等待最终批准时为 `aligning`。无需先有 BA 问卷。`align` 内按设计树连续讨论与更新，每轮只记关键变化、依据与下一步；Q 编号、关键答复与实质修订保留。03 关键问题收敛并获最终批准后进入 `planning`，一般实现细节留给 04。具体命令与回流按 `workflow/overview.md`、`workflow/session-protocol.md`。

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

`stage: done` 后把目录移到 `archive/YYYY-MM/`（按结卡月份）。链接仓库的同名目录一并移动，修正其目标以及日志索引、现行规范等受影响的链接；旧记录中的原始路径保留修订依据并补充归档位置。归档卡是历史卡查询的来源（读卡阶段按主题检索）。

## 示例

接入时可在目标项目内编写 `_example-feat-0000-sample/` 作为格式样板；模板包不包含真实业务卡。对外分享样板时使用虚构模块与数据，不把内部需求或证据一起发布。
