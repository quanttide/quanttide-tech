---
name: devops-release
description: 版本发布技能，遵循语义化版本规范，用于创建 Git 标签、更新 CHANGELOG 并发布 GitHub Release。
---

# devops-release

发布 Git 仓库 Release。

## 规则

- 版本号遵循 semver（MAJOR.MINOR.PATCH）
- 发布前确认工作区干净
- Release notes 只包含对应版本内容
- 发布主仓库前确认所有子模块引用是最新的

## 依赖

- devops-commit: 检查工作区状态
- devops-review: 发布前验证

## 工作流

### 1. 预检查

必须执行，不可跳过：

```bash
# 检查工作区状态
git status

# 检查版本号格式（semver）
VERSION="v0.4.0"
if ! [[ "$VERSION" =~ ^v[0-9]+\.[0-9]+\.[0-9]+(-[a-zA-Z0-9.]+)?$ ]]; then
  echo "错误: 版本号格式错误"
  exit 1
fi

# 检查 CHANGELOG 是否包含目标版本
if ! grep -q "^## \[${VERSION#v}\]" CHANGELOG.md; then
  echo "错误: CHANGELOG.md 未找到版本"
  exit 1
fi

# 检查标签是否已存在
if git tag -l | grep -q "^${VERSION}$"; then
  echo "错误: 标签已存在"
  exit 1
fi
```

### 2. 发布前确认

向用户展示检查结果并请求确认。

### 3. 子模块发布 Release

```bash
cd <子模块路径>
# 执行预检查
git tag <version>
git push origin <version>
gh release create <version> --title "<version>" --notes "..."
```

### 4. 主仓库发布 Release

```bash
# 确认所有子模块已更新
git submodule update --remote

# 更新 CHANGELOG.md
git add CHANGELOG.md && git commit -m "docs: update CHANGELOG for vX.Y.Z"

# 创建标签并推送
git tag <version> && git push origin <version>

# 创建 GitHub Release
gh release create <version> --title "<version>" --notes "..."
```

### 5. 错误处理

```bash
# 回滚标签
git tag -d <version>
git push origin --delete <version>
```

## 常见错误

| 错误 | 原因 | 解决方案 |
|------|------|----------|
| CHANGELOG 缺少版本 | 忘记更新 CHANGELOG.md | 添加版本记录后再发布 |
| 标签已存在 | 重复发布 | 删除旧标签或使用新版本号 |
| 工作区脏 | 有未提交变更 | 提交或暂存变更后再发布 |
| 子模块未更新 | 子模块有新提交 | 执行 `git submodule update --remote` |

## 预发布检查清单

- [ ] 所有子模块版本已锁定
- [ ] 通过 CI 测试
- [ ] CHANGELOG.md 版本段已验证
- [ ] 版本号格式正确
- [ ] Release Notes 提取成功
- [ ] 工作区干净