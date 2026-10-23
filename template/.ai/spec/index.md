# `spec/` 索引 · 开发前必读与质量检查

规范按主题分文件；本索引按**任务类型**告诉你先读哪几份。索引不是目的，被指向的文件才是。

## 文件一览

| 文件 | 内容 | 状态 |
|---|---|---|
| `overview.md` | 系统是什么、边界、干系人、环境与仓库信息 | 待写 |
| `architecture.md` | 模块地图（真实包与代表文件）、请求 / 事件 / 定时链路、关键设计 | 待写 |
| `code-placement.md` | 现状结构；新代码的目标目录与依赖边界；历史位置迁移说明 | 待写 |
| `domain.md` | 实体、状态机、枚举、术语表 | 待写 |
| `conventions.md` | 编码约定与"新增 X 怎么做"配方 | 待写 |
| `integrations.md` | 各上下游在代码里的落点：client、配置键、日志前缀、超时与重试 | 待写 |
| `testing.md` | 测试框架、命令、mock 边界、最低要求 | 待写 |
| `config-and-deploy.md` | 配置来源链、CI 链路、分支与环境、发布检查清单 | 待写 |
| `legacy.md` | 历史包袱清单：现象 / 原因 / 影响 / 建议 / 证据 / 状态 | 待写，持续追加 |
| `guides.md` | 思考清单：跨层、复用、本项目特有触发点 | 待写，持续追加 |

每份写完把"状态"改成"完成"。章节要求见本模板库的 [推广指南](../../../02-推广指南.md) 第 4 步；接入后以目标仓库的事实为准。

## 开发前按任务类型必读

| 本卡要做的事 | 先读 |
|---|---|
| 任何新增/修改代码 | `code-placement.md`、`conventions.md`「最小实现阶梯」 |
| 制定开发计划 / 技术设计 | `conventions.md`「设计默认值」与「最小实现阶梯」 |
| 新增或修改接口 | `conventions.md`「新增接口」、`architecture.md`「请求链路」、`../context/api-contract.md` |
| 新增实体 / 字段 / 表 | `conventions.md`「新增实体与迁移」、`domain.md`、`legacy.md` 的迁移条目 |
| 新增或修改定时任务 / 异步任务 | `conventions.md`「新增定时任务」、`architecture.md` |
| 改某个上下游集成 | `integrations.md` 对应行、`../context/upstream-downstream.md` |
| 改配置键 / 部署清单 | `config-and-deploy.md`、`../decisions/adr/` |
| 修任何 bug | `legacy.md`（先搜模块名）、`testing.md`「修 bug 的反馈回路」 |
| 任何跨仓库的改动 | `../context/api-contract.md`、`../context/related-projects.md` |

<按本项目实际模块继续补行；每行的"先读"都要指向真实存在的章节。>

不管做什么，都读 `guides.md`。

## 质量检查（提交前）

1. `git diff --name-only` 看改了什么，对每个改动区域回头读对应规范。
2. `<门禁命令>` 绿。
3. 测试：新纯逻辑 → 单测；bug → 回归测试；改了行为 → 更新既有测试。
4. `conventions.md`「提交前清单」逐项过。
5. 有没有要写回 `legacy.md` / `guides.md` / `../decisions/` 的新知识。

**语言**：文档中文，代码注释沿用仓库现状。
