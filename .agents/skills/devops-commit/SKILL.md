---
name: commit
description: Git 提交技能，遵循 Conventional Commits 规范，用于创建规范提交。
---

# Git 提交技能

## 提交规范

使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>: <description>
```

### 提交类型

- **feat**：新功能
- **fix**：修复 bug
- **docs**：文档更新
- **test**：测试相关
- **refactor**：代码重构
- **chore**：构建/工具

### 提交示例

```bash
git commit -m "feat: 添加新功能"
git commit -m "fix: 修复登录问题"
git commit -m "docs: 更新 README"
```

## 子模块提交

在子模块中提交并推送到主仓库：

```bash
# 1. 子模块内提交
git -C docs/handbook add -A
git -C docs/handbook commit -m "docs: 更新文档"
git -C docs/handbook push

# 2. 主仓库提交子模块引用更新
git add docs/handbook
git commit -m "chore: update handbook submodule"
git push
```

## 推荐工具

使用 commitizen 交互式创建提交：

```bash
cz commit
```