# AGENTS.md

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

## 特殊文件

| 文件 | 用途 |
|------|------|
| `AGENTS.md` | AI Agent 工作指南（本文档） |
| `CONTRIBUTING.md` | 贡献指南和 SKILL 维护 |
| `README.md` | 项目说明 |
| `ROADMAP.md` | 产品路线图 |
| `CHANGELOG.md` | 版本变更记录 |

## 工作原则

1. 最小干预：仅在用户明确请求时操作
2. 验证优先：修改后检查文件命名和内容
3. 明确命名：严格按照规范命名文件

## 更新流程

当发生错误或问题时，按以下流程处理：

1. **记录问题**：在 CHANGELOG.md 或 GitHub Issue 中记录问题
2. **分析原因**：找出问题根因
3. **修复问题**：提交修复
4. **更新文档**：更新 AGENTS.md、CONTRIBUTING.md 或相关 SKILL
5. **持续改进**：从错误中学习，优化工作流程
