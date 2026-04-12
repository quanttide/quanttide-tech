# CONTRIBUTING

本项目是量潮科技工作手册系统，采用多仓架构管理数字资产。

## 项目结构

见 [README](./README.md)。

## SKILL 维护指南

本项目的 AI Agent 技能存储在 `.agents/skills/` 目录。

SKILL 维护遵循 [Agent Skills 规范](https://agentskills.io/specification)。

### SKILL 目录结构

```
.agents/skills/
├── <skill-name>/
│   └── SKILL.md
```

### SKILL 格式规范

```yaml
---
name: <skill-name>
description: 技能描述，说明使用场景
---
```

### 创建新 SKILL

1. 在 `.agents/skills/` 下创建技能目录
2. 编写 `SKILL.md`，包含 YAML 头和技能说明
3. 参考已有 SKILL 的结构和格式

### 同步 SKILL 到子仓库

稳定的 SKILL 可同步到 gallery 仓库：

```bash
# 复制到 gallery
cp .agents/skills/<skill>/SKILL.md docs/gallery/devops/<skill>/SKILL.md

# 在 gallery 子模块提交
cd docs/gallery
git add devops/<skill>/SKILL.md
git commit -m "docs: add <skill> skill"
git push

# 更新主仓库引用
cd ..
git add docs/gallery
git commit -m "chore: update gallery submodule"
git push
```

---

## .quanttide 配置维护

`.quanttide/` 目录是项目的契约事实源。

### 契约文件

| 文件 | 用途 |
|------|------|
| `.quanttide/asset/contract.yaml` | 数字资产契约 |
| `.quanttide/docs/contract.yaml` | 文档工程契约 |

### 添加新契约

1. 在 `.quanttide/` 下创建对应分类目录
2. 创建 `contract.yaml`，包含契约说明
3. 更新 `.quanttide/README.md` 添加契约索引
4. 提交并推送

### 契约格式

```yaml
# 契约名称
# 模块定位：简述契约用途

# 资产定义
assets:
  <asset-name>:
    title: 资产标题
    type: 资产类型
    path: 资产路径
    description: 资产描述
```

## 工作流程

1. 创建分支：基于 main 创建功能分支
2. 开发：在分支上进行开发
3. 提交：使用 Conventional Commits 格式提交
4. 推送：推送分支并创建 PR