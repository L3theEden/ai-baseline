# AI 开发基线（`.ai/`）

让任意 AI 编码工具按团队敏捷流程（BA 开卡 → 澄清 → 对齐 → 开发 → DC → QA）辅助开发，并把项目规范、历史包袱、上下游上下文与每张卡的决议落成仓库里的 Markdown。

| 文件 | 给谁看 |
|---|---|
| `01-介绍.md` | 想知道它是什么、解决什么问题、如何使用：负责人、BA、QA、Dev |
| `02-推广指南.md` | 要在自己项目上复现：Dev / Tech Lead，10 步 + 验证脚本 + 常见问题 |
| `template/` | 可直接复制到目标仓库根目录的模板包：通用流程与模板已成品，`spec/` 与 `context/` 是带章节要求的骨架 |

只做读卡分析、整理 BA 问卷和回填答复时，使用独立的 [`template-lite/`](template-lite/)；接入步骤和可复制的提示见 [`03-精简版使用指南.md`](03-精简版使用指南.md)。精简版在答复收敛后结束，不接后续开发流程。

文档中的任务管理场景、`DEMO-*` 卡号与示例代码路径均用于说明流程，不对应真实项目。模板里的 `spec/`、`context/` 需要在目标仓库中依据实际代码填写。

设计参考：[Trellis](https://github.com/mindfold-ai/Trellis)、[mattpocock/skills](https://github.com/mattpocock/skills) 与 [ponytail](https://github.com/DietrichGebert/ponytail)，只借结构与原则，不依赖其脚本与运行时。

将基线用于实际业务后，卡片、日志、接口样例与项目规范可能包含内部信息。对外分享前同时检查文件和 Git 历史，使用虚构示例替代真实业务数据，并移除内部地址、个人信息与凭证。
