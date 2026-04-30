---
title: Git Submodule 获取更新状态
---
# Git Submodule 获取更新状态

获取 Git submodule 所有远端仓库的更新状态，而不立即修改本地代码，是一个常见但容易踩坑的需求。

由于 Git submodule 的设计理念是子模块绑定在特定的 commit 上，而不是跟踪分支，因此常规的 `git status` 无法直接告诉你远端是否有新提交。

以下是获取所有子模块远端更新状态的方法，按推荐程度从高到低排列。

## 方法一：最现代、最快捷的方式（Git 2.14+）

这是最符合获取状态但不修改代码语义的命令组合：

```bash
# 1. 获取父仓库及所有子模块的远端最新元数据（不改变代码）
git fetch --recurse-submodules=yes

# 2. 预演（Dry-run）更新操作，仅输出状态报告
git submodule update --remote --dry-run
```

`fetch --recurse-submodules=yes` 会并行去所有子模块的远端拉取最新的提交记录到本地，但不改变工作区。

`update --remote` 默认会将子模块切换到远端的默认分支（通常是 main/master）的最新提交。

`--dry-run` 是核心：它会告诉你如果现在执行更新，哪些子模块会被改变，改变到哪个 commit，但不会真正执行修改。

## 方法二：深入检查具体差异数

如果你不仅想知道有没有更新，还想知道远端到底新增了哪些代码，可以使用 `foreach` 结合 `log`：

```bash
# 1. 先确保拉取了远端最新数据
git fetch --recurse-submodules=yes

# 2. 遍历所有子模块，对比当前 commit 与远端默认分支的差异
git submodule foreach --recursive '
  echo "====== 检查子模块: $name ($path) ======";
  remote_branch=$(git remote show origin | grep "HEAD branch" | awk "{print \$NF}");
  git log --oneline HEAD..origin/$remote_branch;
  echo "";
'
```

优点：直观地展示每个子模块落下了多少个 commit，便于评估是否需要升级。

## 方法三：使用 git status

在执行完 `git fetch --recurse-submodules=yes` 之后，可以直接运行 `git status`。

输出标志说明：

- 子模块前是 `+` 号（例如 `+cba1234 path/to/sub`）：子模块当前的 commit 与父仓库记录的 commit 不一致
- 无加号：父仓库的指针还没指向最新，`git status` 不会报警

所以方法一更精准。

## 避坑指南

永远不要忘记 fetch。很多人直接执行 `git submodule status`，发现没有更新。这是因为没执行 `fetch`，本地的远端分支指针还是旧的。

父仓库并不关心子模块的远端有没有更新，它只锁定当时 `add` 时的那个 commit hash。如果你想更新子模块，流程应该是：

1. `git submodule update --remote`
2. `git add path/to/sub`
3. `git commit -m "update sub"`

子模块的更新必须通过提交父仓库来生效。

如果项目有很多子模块，串行 fetch 会非常慢。建议开启并行配置：

```bash
git config --global submodule.fetchJobs 8
```

子模块默认处于 detached HEAD 状态。最佳实践是不要在子模块的 detached HEAD 下直接开发，应该 checkout 到一个本地分支。

## 一键脚本

可以将以下命令封装成一个 Git Alias，以后只需输入 `git sub-status` 即可：

```bash
git config --global alias.sub-status '!git fetch --recurse-submodules=yes --quiet && git submodule update --remote --dry-run'
```

使用时：

```bash
git sub-status
```

这会静默拉取所有远端信息，并打印出一份干净的哪些子模块将会被更新的报告。
