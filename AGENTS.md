# AGENTS.md - Agent 工作指南

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

## 工作原则

1. **最小干预**: 仅在用户明确请求时操作
2. **原子提交**: 每次提交独立完整
3. **验证优先**: 修改后检查文件命名和内容
4. **明确命名**: 严格按照规范命名文件
5. **反思学习**: 从错误中学习并改进工作流程
6. **写作规范**: 遵循 CONTRIBUTING.md 中的文档写作标准

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