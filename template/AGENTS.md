<!-- AI-BASELINE:START -->
# <项目名> · AI 协作入口

<一句话：本仓库是什么、技术栈、对端仓库在哪>。对端仓库与上下游系统见 `.ai/context/`。

所有 AI 协作知识都在 `.ai/`。本文件只做导航与硬规则，细节以被指向的文档为准。

## 会话开始先读

1. `.ai/README.md`：目录索引、按阶段的阅读顺序、维护规则
2. `.ai/workflow/overview.md`：七阶段流程、需求问答循环与卡状态机
3. `.ai/workflow/session-protocol.md`：每个窗口的开场与收尾动作
4. `.ai/spec/index.md`：按任务类型的"开发前必读"与"质量检查"

## 阶段命令 → 流程文档

阶段命令由用户输入，AI 不自行调用阶段 skill。用户启动 `align` 后，允许在本卡 02–03 之间自动按设计树追问、回填与复核，无需反复输入命令；其余阶段仍由用户另行触发。命令可用薄壳 skill 调用（Claude Code 用 `/<命令>`，其他工具直接说出命令名）。

| 用户输入 | 读并执行 |
|---|---|
| `card-intake`（附卡内容与卡号） | `.ai/workflow/01-card-intake.md` |
| `clarify` | `.ai/workflow/02-clarify.md` |
| `align`（附 BA 答复） | `.ai/workflow/03-align.md` |
| `dev-plan` | `.ai/workflow/04-dev-plan.md` |
| `develop`（协调与评审） | `.ai/workflow/05-develop.md` |
| `execute-subtask <卡目录> <T编号>`（执行一个子任务） | `.ai/workflow/05-execute-subtask.md` |
| `card-review <卡目录> spec\|standards`（卡级代码评审，推送前） | `.ai/workflow/05-card-review.md` |
| `desk-check` | `.ai/workflow/06-desk-check.md` |
| `qa-handoff` | `.ai/workflow/07-qa-handoff.md` |
| 缺上下文 / 不知道对端怎么做 | `.ai/workflow/missing-context.md` |
| 换窗口 / 交接 / 上下文快满 | `.ai/workflow/session-protocol.md` |

## 硬规则（依据见 `.ai/spec/` 与 `.ai/decisions/`）

通用五条，所有项目保留：

- 每张卡先在 `.ai/cards/<feat|fix>-<卡号>-<slug>/` 建目录再动代码；跨仓库的卡，文档放主改动仓库，另一仓库同名目录只放链接。
- 能从代码、配置、测试、git 历史查到的事实自己查；只问用户产品意图、范围边界、风险取舍。
- 默认一个窗口只做一个阶段；`align` 内的需求问答可连续往返 02–03，进度逐轮落档。进入开发计划及后续阶段仍需用户显式命令，"继续""没问题就开发"都不算；换窗口靠卡目录文件交接。
- 建卡目录、对齐批准都不是开发许可：写业务代码或迁移脚本前，必须有 `04-dev-plan.md` 的拆解确认记录（批准人、日期、原话）。
- 本卡提交推送到远端主分支（会触发部署）之前，必须有 `05-card-review.md` 结论为"通过"；提前推送须用户确认并记录原因。

项目特有的（落地时从 `spec/legacy.md` 与 `decisions/adr/` 里挑 3–6 条"违反就出事故"的规则写在这里，每条一句话）：

- <例：表结构只通过新增迁移脚本变更，不改基线脚本>
- <例：时间字段读写必经统一工具类>
- <例：不提交任何 token / secret；部署侧配置在 XX 预建>
- DC 前本地 `<门禁命令>` 必须绿。
- 文档写中文，技术名词、类名、路径保留英文。

## 命令速查

```bash
<构建 + 测试的门禁命令>
<只跑单个测试的命令>
<本地启动命令>
```

本地运行所需环境变量与各环境信息见 `.ai/spec/config-and-deploy.md`。
<!-- AI-BASELINE:END -->
