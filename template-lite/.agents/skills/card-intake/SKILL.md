---
name: card-intake
description: 需求分析精简版读卡：核实卡内容、初判影响面、记录缺失信息，生成卡片分析文档。
disable-model-invocation: true
---

用户请求读卡时，读取并执行 `.ai/README.md` 和 `.ai/workflow/01-card-intake.md`，按 `.ai/templates/card-analysis.md` 写入指定卡目录。此入口只服务精简版需求分析，业务文件保持只读。已有卡先读取再更新。
