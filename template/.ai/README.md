# `.ai/` · <项目名> AI 开发基线

这套目录让任意 AI 编码工具（读 `AGENTS.md` 的工具为主）按团队敏捷流程辅助开发：BA 开卡 → AI 与 Dev 交互澄清并质疑价值、整理本轮 BA 问卷 → Dev 与 BA 多轮对齐 → 顶级模型制定开发计划并拆成子任务 → 执行者（可用低端模型）逐个子任务实现、顶级模型评审 → 产出 DC 文档向 QA/BA 演示 → QA 依卡测试。每批答复后复核新问题、依赖、冲突和验收缺口；明确要求直接出问卷时可跳过访谈。流程按"一个窗口只做一个阶段"运行，阶段之间只靠卡目录里的文件交接。它同时承载项目全量信息、历史包袱与上下游上下文，让每次新会话都从真实背景开始，而不是从零猜。

<多仓库项目：每个仓库一套文件名完全相同的 `.ai/`，内容各自项目化。流程文档两边一致，规范文档各写各的。单仓库项目删掉本段。>

## 目录索引

| 目录 / 文件 | 内容 | 谁维护、何时改 |
|---|---|---|
| `workflow/` | 七个阶段的操作手册 + 缺上下文协议 + 会话协议 | 流程变更时改；两仓库保持一致 |
| `spec/` | 项目规范：概览、架构现状、代码存放与依赖边界、领域、编码约定、集成、测试、配置部署、历史包袱、思考清单 | 每张卡结卡时问"这张卡教会了什么"，把新知识写回来 |
| `context/` | 对端仓库、前后端契约、上下游系统一览 | 契约或上下游变化时改；缺上下文补全后沉淀 |
| `decisions/adr/` | 极简架构决策记录（难回头、事后会困惑、有真实取舍的决定） | 做出此类决定时新增，不改旧条目，用"superseded"标记 |
| `decisions/rejected/` | 被否决的需求 / 价值质疑结论，按概念一文件 | 对齐阶段 BA 否决某方向时写入；再遇同类需求先翻这里 |
| `templates/` | 卡文档模板：问题清单、对齐、开发计划、子任务单、开发记录、卡级代码评审、DC、日志条目 | 模板不够用时改，改完同步另一仓库 |
| `cards/` | 每张卡一个目录，编号文件 `01`…`06` + `tasks/`；做完移入 `archive/YYYY-MM/` | 卡生命周期内持续更新 |
| `journal/` | 按开发者分文件的会话日志；每月提炼进 `spec/` 或 `decisions/` | 每次会话结束追加 |

## 按阶段的阅读顺序

| 阶段 | 必读 | 选读 |
|---|---|---|
| 读卡 | `workflow/01-card-intake.md`、`spec/overview.md`、`spec/domain.md` | `decisions/rejected/`、`cards/archive/` 里的同主题卡 |
| 拆问题 | `workflow/02-clarify.md`、`spec/legacy.md`、`context/upstream-downstream.md` | `spec/architecture.md` |
| 对齐 | `workflow/03-align.md` | `decisions/adr/` |
| 制定开发计划 | `workflow/04-dev-plan.md`、`spec/index.md`（按任务类型跳转）、`spec/conventions.md`、`context/api-contract.md` | `spec/guides.md`、`spec/integrations.md` |
| 开发（协调与评审） | `workflow/05-develop.md` | `spec/testing.md` |
| 开发（执行子任务） | `workflow/05-execute-subtask.md`、子任务单及其"先读"列出的文件 | 无（只依据单子工作） |
| 开发（卡级代码评审） | `workflow/05-card-review.md`、`spec/index.md`"质量检查"指向的规范 | `spec/guides.md` |
| DC | `workflow/06-desk-check.md`、`spec/config-and-deploy.md` | `spec/testing.md` |
| 交 QA / 结卡 | `workflow/07-qa-handoff.md`、`journal/README.md` | `spec/legacy.md`（是否要新增条目） |

## 按角色

- **Dev**：全部。
- **BA**：`spec/overview.md`、`spec/domain.md`、每张卡的 `02-questions.md` 与 `03-alignment.md`。
- **QA**：每张卡的 `03-alignment.md`（验收标准）与 `06-desk-check.md`（演示脚本、QA 关注点、数据准备）。

## 五条原则（借自 Trellis，适配本团队）

1. 先规划后写码：没有拆解确认在案的开发计划，不写业务代码。
2. 一个窗口只做一个阶段：阶段命令只能由人触发，AI 不自行推进；阶段之间只靠卡目录里的文件交接。
3. 规范靠文档注入，不靠记忆：写码前按 `spec/index.md` 读对应规范，而不是凭印象。
4. 一切落文件：问题、决议、调研、教训都写进卡目录或 `spec/`；执行者看不到聊天记录，没写进文件的结论等于没发生。
5. 结卡时写回：新约定、新坑、新决策沉淀到 `spec/`、`decisions/`、`journal/`。

## 参考与致谢

- [mindfold-ai/Trellis](https://github.com/mindfold-ai/Trellis)：workflow / spec / tasks / workspace 的分层，"建任务同意 ≠ 实现同意"的门禁，before-dev 的改动边界声明，check 的范围纪律，break-loop 的根因分类。
- [mattpocock/skills](https://github.com/mattpocock/skills)：`grilling` 的设计树轮询、`to-questionnaire` 的问卷格式、`to-spec` / `to-tickets` 的规格与切片、`tdd` 与 `diagnosing-bugs` 的反馈回路、`triage` 与 `.out-of-scope/` 的否决记忆、`domain-modeling` 的术语表与极简 ADR、`writing-for-agents` 的入口文件写法、`pr` 的证据分级、`improve-codebase-architecture` 的摩擦驱动结构复核（热点、deletion test、一次一个模块、行为不变证明）。
- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)（MIT）：最小实现阶梯（写码前逐级停下），只摘编文本、注明出处；只裁实现，不裁测试与契约。

本基线只借结构与原则，不依赖这些来源的脚本、hook 或运行时；全部为纯 Markdown。
