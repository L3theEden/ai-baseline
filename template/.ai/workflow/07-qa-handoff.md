# 07 · 交 QA 与结卡（QA Handoff）

QA 依据 `03-alignment.md` 的 AC 与 `06-desk-check.md` 的演示脚本测试。本阶段处理 QA 反馈、关闭卡、把经验写回基线。

## QA 反馈处理

- **通过**：在 `06-desk-check.md` 的"QA 结果"段逐条 AC 回填通过 / 日期 / 测试人。
- **缺陷，属于本卡 AC 范围**：`stage` 回到 `in-dev`，在 `05-dev-log.md` 追加"QA 修复轮次"，按需新增修复子任务单（编号接着排），走 05 的派发与评审，修复后重新走 06 的对应 AC。
- **缺陷源于设计**：`stage` 回到 `planning`，在新窗口修改开发计划并重新确认。
- **缺陷，超出本卡 AC**：新开 `fix` 卡，`README.md` 的 `links` 引用原卡；原卡不因它阻塞。
- **QA 质疑 AC 本身**：回到 03 与 BA 重新对齐，不在开发阶段私下改 AC。

## 结卡清单（全部 AC 通过后）

1. **写回 spec。** 问自己："这张卡教会了什么，未来的 AI 或同事不知道会再踩一次？"逐项判断并落笔：
   - 新约定或新配方 → `spec/conventions.md`
   - 对齐文档"术语"一节里新定下的词 → `spec/domain.md` 的术语表
   - 新坑、临时方案、被迫的妥协 → `spec/legacy.md`（写现象 / 原因 / 影响 / 处理建议 / 证据 / 状态）
   - 难回头且有真实取舍的决定 → `decisions/adr/`（极简格式，见该目录 README）
   - 被否决的方向 → `decisions/rejected/`
   - 契约变化 → `context/api-contract.md`；上下游行为变化 → `context/upstream-downstream.md`
   - 新的"改 X 前要想到 Y" → `spec/guides.md`
   结论是"没有要写的"也可以，但要走一遍判断并在 journal 里写明。`05-dev-log.md` 的偏差段记录了计划与实际的差异，是最重要的回写来源。
2. **bug 卡加做根因分析。** 根因五类：缺规范 / 跨层契约不清 / 改一处漏一处 / 测试盲区 / 隐含假设。写明预防机制（文档、类型、测试、检查清单）并落实到对应文件。
3. **写 journal。** 按 `journal/README.md` 追加本卡条目（模板 `templates/journal-entry.md`）。
4. **归档。** `stage: done`，卡目录移到 `.ai/cards/archive/YYYY-MM/`，链接仓库的同名目录一并移动。
5. **提交。** 文档改动与代码分开提交，信息带卡号。

## 完成标准

- QA 结果已回填，`stage: done`，目录已归档。
- spec / decisions / journal 的回写已完成或已明确"无需回写"。
