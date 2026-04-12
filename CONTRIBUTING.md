# CONTRIBUTING

本项目是量潮科技工作手册系统，采用多仓架构管理数字资产。

## 项目结构

见 [README](./README.md)。

## SKILL 维护指南

本项目的 AI Agent 技能存储在 `.agents/skills/` 目录。

### SKILL 目录结构

```
.agents/skills/
├── <skill-name>/
│   └── SKILL.md
```

### 创建新 SKILL

1. 在 `.agents/skills/` 下创建技能目录
2. 编写 `SKILL.md`，包含：
   - YAML 头：`name`、`description`
   - 技能说明和使用方法

### SKILL 格式规范

```yaml
---
name: <skill-name>
description: 技能描述，说明使用场景
---
```

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

## 子模块操作

### 更新子模块

```bash
# 查看子模块状态
git submodule status

# 更新所有子模块
git submodule update --init --recursive

# 在子模块中提交并推送
git -C <子模块路径> commit -m "message"
git -C <子模块路径> push
```

### 提交子模块更新

1. 在子模块中提交并推送
2. 在主仓库提交子模块引用更新

```bash
git -C docs/handbook add -A
git -C docs/handbook commit -m "feat: update content"
git -C docs/handbook push

git add docs/handbook
git commit -m "chore: update handbook submodule"
git push
```

## 工作流程

1. 创建分支：基于 main 创建功能分支
2. 开发：在分支上进行开发
3. 提交：使用 Conventional Commits 格式提交
4. 推送：推送分支并创建 PR
