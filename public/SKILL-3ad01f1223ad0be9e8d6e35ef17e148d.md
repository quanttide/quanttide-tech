---
name: devops-review
description: 审查仓库状态、CHANGELOG、版本一致性等，支持发布前检查、代码审查、文档审查等多场景。
---

# devops-review

统一审查仓库状态，为多种工作流程提供前置检查。

## 功能

- 验证 CHANGELOG.md 版本连续性
- 检查未追踪文件
- 验证子模块状态
- 检查标签与代码一致性
- 验证版本号格式

## 使用场景

- 发布前验证
- 定期健康检查
- CI/CD 流水线检查

## 验证项

### 版本号格式验证

```bash
validate_version_format() {
  local VERSION="$1"
  
  if [[ "$VERSION" =~ ^v[0-9]+\.[0-9]+\.[0-9]+(-[a-zA-Z0-9.]+)?$ ]]; then
    echo "✓ 版本号格式正确: $VERSION"
    return 0
  else
    echo "✗ 版本号格式错误: $VERSION"
    echo "  预期格式: vX.Y.Z 或 vX.Y.Z-qualifier"
    return 1
  fi
}
```

### CHANGELOG 验证

验证 CHANGELOG.md 中版本存在且有内容。

### 工作区状态验证

检查是否有未提交变更。

### 子模块状态验证

检查子模块是否初始化及是否有新提交。

### 标签验证

检查标签是否已存在。

### 远程仓库验证

检查远程仓库连接。

## 完整验证流程

```bash
validate_release() {
  local VERSION="$1"
  local ERRORS=0
  
  validate_version_format "$VERSION" || ((ERRORS++))
  validate_changelog "$VERSION" || ((ERRORS++))
  validate_working_directory || ((ERRORS++))
  validate_submodules || ((ERRORS++))
  validate_tag "$VERSION" || ((ERRORS++))
  validate_remote || ((ERRORS++))
  
  if [ "$ERRORS" -eq 0 ]; then
    echo "✓ 所有验证通过，可以发布"
    return 0
  else
    echo "✗ 发现 $ERRORS 个错误"
    return 1
  fi
}
```

## 集成

在 devops-release 预检查中调用。