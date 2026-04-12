# AGENTS.md

详细操作指南见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## SKILL 快速索引

| 场景 | SKILL 位置 |
|------|-----------|
| 提交代码 | `.agents/skills/devops-commit/SKILL.md` |
| 发布版本 | `.agents/skills/devops-release/SKILL.md` |
| 文档格式 | `.agents/skills/docs-format/SKILL.md` |
| 子模块操作 | `.agents/skills/devops-submodule/SKILL.md` |

## 契约文件

| 文件 | 用途 |
|------|------|
| `.quanttide/asset/contract.yaml` | 数字资产契约 |
| `.quanttide/docs/contract.yaml` | 文档工程契约 |

AI Agent 进入仓库后，先读取 `.quanttide/` 目录获取上下文。

## 工作原则

1. 最小干预：仅在用户明确请求时操作
2. 验证优先：修改后检查文件命名和内容
3. 明确命名：严格按照规范命名文件
4. 反思学习：从错误中学习并改进工作流程
