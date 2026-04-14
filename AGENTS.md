# AGENTS.md

## SKILL 快速索引

| 场景 | SKILL 位置 | 触发时机 |
|------|-----------|----------|
| 提交代码 | `.agents/skills/devops-commit/SKILL.md` | 用户请求提交代码时（含子模块提交） |
| 发布版本 | `.agents/skills/devops-release/SKILL.md` | 用户请求发布新版本、打标签时 |
| 流程审查 | `.agents/skills/devops-review/SKILL.md` | 发布前审查、代码审查、文档审查时 |
| 文档格式 | `.agents/skills/docs-format/SKILL.md` | 操作 Markdown 文档时 |
| 子模块操作 | `.agents/skills/devops-submodule/SKILL.md` | 操作 Git 子模块（更新、提交子模块）时 |

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
4. 持续反思：从错误中学习，优化工作流程
