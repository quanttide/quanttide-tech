# AGENTS.md - Agent 工作指南

## 事实源

### 程序型记忆五层体系

| 层次 | 名称 | 说明 | 文件 |
|------|------|------|------|
| L1 | Paper | 工作论文：日志规范原理 | `meta/paper/journal.md` |
| L3 | Handbook | 学习日志手册 | `meta/handbook/learn_journal.md` |
| L5 | Bylaw | 学习日志章程 | `meta/bylaw/learn_journal.md` |

## 快速索引

| 场景 | 命令/操作 |
|------|----------|
| 更新子模块 | `git submodule update --init --recursive` |
| 推送所有子模块 | `for m in docs/* src/*; do git -C "$m" push 2>/dev/null; done` |
| 提交子模块更新 | `git add <子模块> && git commit -m "chore: update <子模块>"` |
| 创建规范提交 | `cz commit` |

## 使用场景

### 1. 文档更新
- 修改 `docs/` 下的子模块内容
- 在子模块内提交：`git -C docs/handbook commit -m "docs: update content"`
- 在子模块内推送：`git -C docs/handbook push`
- 更新主仓库引用：`git add docs/handbook && git commit -m "chore: update handbook submodule"`

### 2. 代码开发
- 修改 `src/` 下的子模块
- 遵循子模块内的 AGENTS.md 规范
- 提交时使用 Conventional Commits 格式

### 3. 学习日志
- 按 L1→L3→L5 路径学习
- 先读 `meta/paper/journal.md`，再读 `meta/handbook/learn_journal.md`
- 最终遵循 `meta/bylaw/learn_journal.md`

## 工作原则

1. **最小干预**: 仅在用户明确请求时操作
2. **原子提交**: 每次提交独立完整
3. **验证优先**: 修改后检查文件命名和内容
4. **明确命名**: 严格按照规范命名文件
5. **反思学习**: 从错误中学习并改进工作流程

## 如何更新 AGENTS.md

当项目工作流程变更时，需要更新本文件：

1. **确定变更类型**：
   - 新增使用场景 → 添加到「使用场景」表格
   - 新增命令/操作 → 添加到「快速索引」表格
   - 原则变更 → 更新「工作原则」

2. **更新流程**：
   - 直接修改本文件
   - 提交时使用 `docs: update AGENTS.md` 或 `chore: update AGENTS.md`
   - 推送后自动生效

3. **保持简洁**：
   - 目标长度约 50 行
   - 优先引用子模块的 AGENTS.md
   - 使用表格增强可读性