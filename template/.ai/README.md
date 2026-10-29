# `.ai/` · <项目名> AI 开发基线

这套目录让 AI 与 Dev 从已有事实出发协作：读卡 → 沿设计树讨论需求与关键取舍 → 整理共识 → 制定开发计划 → 开发与评审 → DC → QA。需要业务判断时才提炼问题给 BA，明确的原卡要求与 Dev 职责内的技术决定直接记录。每轮简述变化、影响与下一步，`align` 中发现缺口直接继续讨论；不要求先有 BA 问卷或答复。完整流程默认分阶段使用会话，02–03 可连续问答，最终对齐仍保留一次阶段确认。进度与项目知识落入文件，换会话从卡目录续接。

<多仓库项目：每个仓库使用同一套目录约定，内容各自项目化。通用流程同步，项目适配分别登记；规范各写各的，共享契约指定主维护位置。单仓库项目删掉本段。>

## 目录索引

| 目录 / 文件 | 内容 | 谁维护、何时改 |
|---|---|---|
| `workflow/` | 完整七阶段、轻量维护手册及共用协议 | 流程变更时按文件归属合并；项目适配留记录 |
| `spec/` | 项目现状与工程规范：架构、代码归属、领域、约定、集成、测试、部署、历史包袱、思考清单 | 随已验证的实现更新；结卡提炼可复用经验 |
| `context/` | 对端仓库、现行共享契约、上下游系统一览 | 查证或实现变化后更新；镜像记录主来源与修订 |
| `decisions/adr/` | 极简架构决策记录（难回头、事后会困惑、有真实取舍的决定） | 做出此类决定时新增，不改旧条目，用"superseded"标记 |
| `decisions/rejected/` | 被否决的需求 / 价值质疑结论，按概念一文件 | 对齐阶段 BA 否决某方向时写入；再遇同类需求先翻这里 |
| `templates/` | 完整卡各阶段模板、轻量维护记录及日志条目 | 模板不够用时改；按登记的适配同步 |
| `cards/` | 每卡一个目录；完整流程用阶段产物，轻量用 `maintenance.md`；做完归档 | 卡生命周期内持续更新 |
| `journal/` | 按开发者分目录、按月分卷的会话日志；需要时建立轻量索引 | 每次会话结束追加；每月复查提炼去向 |

## 轻量维护入口

预期明确、单仓库且风险低的小修复，用户可输入 `maintain <问题描述或维护卡目录>`，或明确要求按轻量维护处理。适用条件、实现授权和升级规则见 [轻量维护](workflow/maintenance.md)，集中记录在 `maintenance.md`；可同一窗口完成核实、修复、验证与评审。

卡 README 用 `workflow: maintenance` 区分；缺省仍是完整流程 `full`。未结项完整卡的原范围缺陷沿原卡回流，已归档卡的新问题建立关联记录。涉及业务规则、权限、数据迁移、共享契约、并发等变化时升级，已授权动作无需重复确认，未授权的提交 / 推送不自动执行。

## 最小实现与修复

完整流程与轻量维护共用 [最小实现与修复原则](workflow/implementation-principles.md)：先核实必要性和现有能力，再写最小且清晰的实现；修 bug 前查调用链与相关入口；有意简化时记录当前足够的依据、已知上限和重新评估条件。核查与取舍写进现有计划 / 维护记录，已实施的持续限制写回 `spec/legacy.md`。通用正文随基线提供，项目约定与适配仍在 `spec/conventions.md`。

## 项目文档怎么保持有效

按 [项目文档维护](workflow/documentation.md) 区分现行事实、工程约定、本卡目标与历史。读取时遇到事实冲突，或本卡影响长期文档时，先读该说明。完整流程在 04 列文档影响，05 随实现更新并评审，06 核对验证范围，07 提炼与归档；轻量维护将相同责任集中记入 `maintenance.md`，不额外生成 04/05。关键事实注明来源与核实范围；计划获批、代码已实现、已部署、环境已验证分别记录。

规范按 [触发条件与阅读目的](spec/index.md#开发前按任务类型必读) 定位真实章节。长期正文保留语义、边界和来源；可查询清单用主来源指针。换会话先读卡片的 [当前恢复摘要](cards/README.md#当前恢复摘要)，历史按需检索；日志分卷与提炼状态见 [journal 规则](journal/README.md)。文档变更使用现有工具和 [人工检查项](workflow/documentation.md#文档检查) 核验。

## 基线来源与项目适配

由接入 / 升级者在目标项目填写；本模板中的“未登记”不代表已完成接入。来源修订指模板仓库的固定提交，填写方法及文件归属见 [完整版基线来源与升级](workflow/baseline-upgrade.md)。

| 项 | 值 |
|---|---|
| 来源仓库 | https://github.com/L3theEden/ai-baseline |
| 模板目录 | `template/`（完整版） |
| 来源修订 | 未登记 |
| 最后完整同步日期 | 未登记 |

**项目适配**：首次接入填写具体文件 / 章节、调整内容与保留原因；没有则写“无”。

| 文件 / 章节 | 项目调整与原因 |
|---|---|

**同步记录**：首次接入或升级完成后填写；部分升级记录目标修订、已处理文件和待处理项，不改写“最后完整同步”的信息。

| 日期 | 旧来源 → 新来源 / 目标修订 | 完整 / 部分 | 变更范围、保留适配与验证结果 |
|---|---|---|---|

## 按阶段的阅读顺序

| 阶段 | 必读 | 选读 |
|---|---|---|
| 轻量维护 | `workflow/maintenance.md`、维护记录、`spec/index.md` 指向的相关章节 | 原卡的有效 AC / 契约及必要证据 |
| 读卡 | `workflow/01-card-intake.md`、`spec/overview.md`、`spec/domain.md` | `decisions/rejected/`、`cards/archive/` 里的同主题卡 |
| 澄清 | `workflow/02-clarify.md`、`spec/legacy.md`、`context/upstream-downstream.md` | `spec/architecture.md` |
| 对齐 | `workflow/03-align.md`、`workflow/02-clarify.md`（与 Dev 沿设计树讨论） | `decisions/adr/` |
| 制定开发计划 | `workflow/04-dev-plan.md`、`spec/index.md` 指向的相关章节与通用约束 | 涉及契约 / 集成时读取 `context/api-contract.md` / `spec/integrations.md` 的相关章节 |
| 开发（协调与评审） | `workflow/05-develop.md` | `spec/testing.md` |
| 开发（执行子任务） | `workflow/05-execute-subtask.md`、子任务单及其“先读”列出的章节与契约 | 缺必要上下文时由协调者补单 |
| 开发（卡级代码评审） | `workflow/05-card-review.md`、`spec/index.md`"质量检查"指向的规范 | `spec/guides.md` |
| DC | `workflow/06-desk-check.md`、`spec/config-and-deploy.md` | `spec/testing.md` |
| 交 QA / 结卡 | `workflow/07-qa-handoff.md`、`journal/README.md` | `spec/legacy.md`（是否要新增条目） |

阶段手册必须读取；项目资料按触发条件定位相关章节，“选读”条件一旦命中即为本卡必读。不得因精简上下文省略通用约束、必要契约或批准记录。

## 按角色

- **Dev**：全部。
- **BA**：`spec/overview.md`、`spec/domain.md`、完整卡的 `02-questions.md` 中待业务判断的部分与 `03-alignment.md`。轻量路径沿用明确预期，出现新的业务决定则升级。
- **QA**：完整卡的 `03-alignment.md` 与 `06-desk-check.md`；轻量维护中项目要求 QA 时，查看 `maintenance.md` 的验收依据与验证记录。

## 五条原则（借自 Trellis，适配本团队）

1. 先明确范围与授权：完整流程须有拆解确认在案的开发计划；轻量须有分流依据与本次实现授权。
2. 按路径推进：完整流程按阶段触发，`align` 可连续问答；轻量可同窗口完成授权内维护。两者都落档，换窗口靠卡目录文件交接。
3. 规范靠文档注入，不靠记忆：写码前按 `spec/index.md` 读对应规范，而不是凭印象。
4. 一切落文件：问题、决议、调研、教训都写进卡目录或 `spec/`；执行者看不到聊天记录，没写进文件的结论等于没发生。
5. 随变化维护：已实现事实及时写回 `spec/`、`context/`；结卡提炼新约定、新坑、新决策并归档。

## 参考与致谢

- [mindfold-ai/Trellis](https://github.com/mindfold-ai/Trellis)：workflow / spec / tasks / workspace 的分层，"建任务同意 ≠ 实现同意"的门禁，before-dev 的改动边界声明，check 的范围纪律，break-loop 的根因分类，update-spec 的契约变化与知识回写时机。
- [mattpocock/skills](https://github.com/mattpocock/skills)：`grilling` 的设计树轮询、`to-questionnaire` 的问卷格式、`wayfinder` 对待展开问题 / 待细化领域 / 范围外的区分、`to-spec` / `to-tickets` 的规格与切片、`tdd` 与 `diagnosing-bugs` 的反馈回路、`triage` 与 `.out-of-scope/` 的否决记忆、`domain-modeling` 的术语表与极简 ADR、`writing-for-agents` 的入口文件写法、`pr` 的证据分级、`improve-codebase-architecture` 的摩擦驱动结构复核（热点、deletion test、一次一个模块、行为不变证明）。
- [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)（MIT）：最小实现阶梯、修复前调用链核查、简化方案的上限与重新评估条件；文本原则按本基线改写，来源修订见 [通用正文](workflow/implementation-principles.md#参考来源)，保留测试、契约与授权边界。

本基线只借结构与原则，不依赖这些来源的脚本、hook 或运行时；全部为纯 Markdown。
