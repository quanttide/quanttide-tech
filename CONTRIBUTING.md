# CONTRIBUTING

## 项目结构

本仓库为 monorepo，包含以下子模块：

| 子模块 | 路径 | 说明 |
|--------|------|------|
| docs/archive | `docs/archive/` | 历史文档归档 |
| docs/bylaw | `docs/bylaw/` | 章程文档 |
| docs/essay | `docs/essay/` | 随笔文章 |
| docs/handbook | `docs/handbook/` | 学习手册 |
| docs/journal | `docs/journal/` | 工作日志 |
| docs/profile | `docs/profile/` | 产品构型档案 |
| docs/report | `docs/report/` | 运营报告 |
| docs/roadmap | `docs/roadmap/` | 产品路线图 |
| docs/tutorial | `docs/tutorial/` | 教程文档 |
| src/qtadmin | `src/qtadmin/` | qtadmin 项目 |
| src/qtcloud-data | `src/qtcloud-data/` | qtcloud-data 项目 |

## 提交规范

使用 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>: <description>
```

### 提交类型

| 类型 | 说明 | 示例 |
|------|------|------|
| feat | 新功能 | `feat: add user authentication` |
| fix | 修复 bug | `fix: resolve null pointer exception` |
| docs | 文档更新 | `docs: update README` |
| test | 测试相关 | `test: add unit tests for api` |
| refactor | 代码重构 | `refactor: simplify logic` |
| chore | 构建/工具 | `chore: update dependencies` |

### 推荐工具

使用 commitizen 创建规范提交：

```bash
# 交互式创建提交
cz commit

# 自动版本升级
cz bump
```

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

```bash
# 1. 在子模块中提交并推送
git -C docs/handbook add -A
git -C docs/handbook commit -m "feat: update content"
git -C docs/handbook push

# 2. 在主仓库提交子模块引用更新
git add docs/handbook
git commit -m "chore: update handbook submodule"
git push
```

## 工作流程

1. **创建分支**: 基于 `main` 创建功能分支
2. **开发**: 在分支上进行开发
3. **提交**: 使用 Conventional Commits 格式提交
4. **推送**: 推送分支并创建 PR（或在子模块中直接推送）