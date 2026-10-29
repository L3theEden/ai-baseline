<!-- AI-BASELINE:START -->
# <项目名> · AI 协作入口

<一句话：本仓库是什么、技术栈、对端仓库在哪>。知识与上下游上下文在 `.ai/`；本文件只做导航与硬规则，细节以被指向的文档为准。

## 会话开始先读

1. `.ai/README.md`：目录索引、按阶段的阅读顺序、维护规则
2. `.ai/workflow/overview.md`：完整 / 轻量维护的分流、需求问答循环与卡状态
3. `.ai/workflow/session-protocol.md`：每个窗口的开场与收尾动作
4. `.ai/spec/index.md`：触发条件、真实文件 / 章节与读取目的，以及提交前质量检查

## 阶段命令 → 流程文档

入口由用户指定，AI 不自行调用 skill。完整流程的 `align` 可连续完成 02–03 问答，其余阶段由用户触发；`maintain` 按轻量协议在已授权范围内连续处理。Claude Code 用 `/<命令>`，其他工具可直接说出命令名。

| 用户输入 | 读并执行 |
|---|---|
| `maintain`（问题描述或维护卡目录） | `.ai/workflow/maintenance.md` |
| `card-intake`（附卡内容与卡号） | `.ai/workflow/01-card-intake.md` |
| `clarify` | `.ai/workflow/02-clarify.md` |
| `align`（可附 Dev 补充、资料或 BA 答复） | `.ai/workflow/03-align.md` |
| `dev-plan` | `.ai/workflow/04-dev-plan.md` |
| `develop`（协调与评审） | `.ai/workflow/05-develop.md` |
| `execute-subtask <卡目录> <T编号>`（执行一个子任务） | `.ai/workflow/05-execute-subtask.md` |
| `card-review <卡目录> spec\|standards`（卡级代码评审，推送前） | `.ai/workflow/05-card-review.md` |
| `desk-check` | `.ai/workflow/06-desk-check.md` |
| `qa-handoff` | `.ai/workflow/07-qa-handoff.md` |
| 缺上下文 / 不知道对端怎么做 | `.ai/workflow/missing-context.md` |
| 换窗口 / 交接 / 上下文快满 | `.ai/workflow/session-protocol.md` |
| 项目文档变化 / 文档与实现冲突 | `.ai/workflow/documentation.md` |
| 首次登记来源 / 升级完整版基线 | `.ai/workflow/baseline-upgrade.md` |

## 通用硬规则（所有项目保留，依据见 `.ai/spec/` 与 `.ai/decisions/`）

- 每张卡先在 `.ai/cards/<feat|fix>-<卡号>-<slug>/` 建目录再动代码；跨仓库的卡，文档放主改动仓库，另一仓库同名目录只放链接。
- 能从代码、配置、测试、git 历史查到的事实自己查；与 Dev 沿设计树讨论需求和技术取舍，业务歧义或规则变更才提炼给 BA。原卡明确要求直接沿用，未知技术事实不自动转交 BA。
- 先读卡的 `workflow`（缺省 `full`）与 `stage`。完整流程按阶段触发，`align` 可连续问答；`maintenance` 可同窗口完成授权内维护。已有完整卡不降级，换窗口靠文件交接。
- 写业务代码前，完整流程须有 `04-dev-plan.md` 的拆解确认；轻量须有 `maintenance.md` 的适用依据与本次实现授权。建目录不等于授权；命中升级条件就转完整流程，不能伪造批准。
- 推送须获授权并通过本次验证与评审：完整流程看 `05-card-review.md`，轻量看 `maintenance.md`。完整流程提前推送须用户确认并记原因；不把修复授权推定为提交或推送授权。

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
