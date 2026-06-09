---
name: devops-code-sync
description: 使用 qtcloud-devops CLI 同步子模块指针到父仓库，实现子模块内容变更后的引用同步与推送。
---

# devops-code-sync

使用 `qtcloud-devops code sync` 命令同步子模块指针到父仓库。

## 命令参考

```
qtcloud-devops code sync [OPTIONS] [NAME] [REPO]
```

| 参数 | 说明 |
|------|------|
| `NAME` | 子模块名称（省略则同步全部） |
| `REPO` | 目标仓库路径（默认当前目录 `.`） |
| `--dry-run` | 预览模式，不实际执行 |

## 工作流

### 1. 检查状态（前置操作）

同步前应先检查子模块状态，确认哪些子模块有更新：

```bash
qtcloud-devops code status
```

该命令会展示以下状态：
| 状态 | 含义 | 颜色 |
|------|------|------|
| `Clean` | 子模块已同步、无未提交变更 | ✅ |
| `Dirty` | 子模块内有未提交的修改 | 🔴 |
| `BehindRemote` | 本地落后远程 | ⬇ |
| `Detached` | 处于游离 HEAD 状态 | ⚠ |
| `Orphaned` | 父仓库记录的提交在远程已不存在 | 💀 |

需要关注的类型：
- **Dirty**：子模块内有未提交变更，须先提交再同步
- **BehindRemote**：子模块落后远程，须先更新到最新
- **Orphaned**：需手动干预

### 2. 执行同步

```bash
# 同步所有子模块
qtcloud-devops code sync

# 同步特定子模块
qtcloud-devops code sync docs/bylaw

# 预览模式（不实际执行）
qtcloud-devops code sync --dry-run docs/bylaw

# 指定仓库路径
qtcloud-devops code sync docs/bylaw /path/to/repo
```

### 3. 验证结果

```bash
# 确认子模块指针已更新
git status

# 查看最新提交
git --no-pager log -1 --oneline
```

## 常见错误与处理

| 错误现象 | 原因 | 处理方式 |
|----------|------|----------|
| `fatal: not on a branch` | 子模块处于游离 HEAD | 先进入子模块 `git checkout main` 再同步 |
| `push 失败: gnutls_handshake` | 代理/网络问题 | 使用 `-c http.proxy="" -c https.proxy=""` 绕过代理 |
| `push-parent 失败` | 父仓库推送失败 | 检查父仓库远程 URL 和网络连接 |
| `Orphaned` | 远程已不存在该 commit | 手动更新子模块到有效提交 |
| `fatal: unable to access` | 远程仓库不可达 | 检查网络及认证状态 |

## 与 devops-submodule 技能的关系

`devops-code-sync` 与 `devops-submodule` 互补：

| 场景 | 使用技能 |
|------|----------|
| 子模块内提交变更 | `devops-submodule` |
| 批量同步子模块指针到父仓库 | `devops-code-sync` |
| 添加/删除子模块 | `devops-submodule` |

典型配合流程：

```bash
# 1. 在子模块内提交变更
cd docs/bylaw
git add -A
git commit -m "docs: update bylaw content"
git push

# 2. 返回主仓库，同步指针
cd /path/to/main
qtcloud-devops code sync docs/bylaw
```

## 使用示例

### 示例一：同步单个子模块

```bash
# 检查子模块状态
qtcloud-devops code status

# 预览要同步的内容
qtcloud-devops code sync --dry-run docs/handbook

# 执行同步
qtcloud-devops code sync docs/handbook
```

### 示例二：遇到游离 HEAD 时的处理

```bash
# 发现游离 HEAD
qtcloud-devops code status
# → apps/qtadmin  Detached  main

# 修复游离 HEAD
cd apps/qtadmin
git checkout main
git pull

# 再执行同步
cd /path/to/main
qtcloud-devops code sync apps/qtadmin
```

### 示例三：网络代理问题

```bash
# 使用代理绕过参数
GIT_HTTP_PROXY="" GIT_HTTPS_PROXY="" qtcloud-devops code sync
```
