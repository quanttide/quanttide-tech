---
name: release
description: 版本发布技能，遵循语义化版本规范，用于创建 Git 标签、更新 CHANGELOG 并发布 GitHub Release。当需要发布新版本、打标签、更新发布说明时使用。
---

# 版本发布技能

用于 quanttide-gallery-of-business-entity 仓库的版本发布流程。

## 发布前检查

1. 检查未发布内容:
   ```bash
   git log <last-version>..HEAD --oneline
   ```

2. 确认发布就绪:
   - [ ] 所有测试通过
   - [ ] 文档已更新
   - [ ] 无未提交的变更
   - [ ] CHANGELOG已更新
   - [ ] 版本号符合语义化版本规范

## 更新 CHANGELOG

1. 编辑 `CHANGELOG.md`:
   ```markdown
   # CHANGELOG

   ## [Unreleased]

   ## [<version>] - <date>

   ### Added
   - 新增功能列表

   ### Changed
   - 修改内容列表

   ### Fixed
   - 修复问题列表

   ### Removed
   - 移除内容列表
   ```

2. 内容要求:
   - 简洁明了，避免冗余描述
   - 使用动词开头：「新增」「修改」「修复」「移除」
   - 每条记录一行，不超过50字
   - 按重要性排序

3. 提交并推送:
   ```bash
   git add CHANGELOG.md
   git commit -m "chore: update CHANGELOG for <version>"
   git push origin main
   ```

## 创建 Git 标签

1. 创建附注标签:
   ```bash
   git tag -a <version> -m "Release version <version-no-v>"
   ```
   其中 `<version-no-v>` 为不带 `v` 前缀的版本号（如 `0.0.2`）

2. 推送标签到远程:
   ```bash
   git push origin <version>
   ```

## 创建 GitHub Release

使用 GitHub CLI 创建 Release:

```bash
gh release create <version> \
  --title "<version>" \
  --generate-notes
```

Release URL: `https://github.com/quanttide/quanttide-gallery-of-business-entity/releases/tag/<version>`

## 发布后确认

- [ ] Git标签已创建并推送
- [ ] GitHub Release已创建
- [ ] Release notes内容准确
- [ ] 主仓库子模块引用已更新

## 版本号规则

遵循语义化版本: `主版本.次版本.修订号`

- **主版本（Major）**: 不兼容的API修改
- **次版本（Minor）**: 向后兼容的功能新增
- **修订号（Patch）**: 向后兼容的问题修复

### 预发布版本

- Alpha版本：`v0.0.1-alpha.1`
- Beta版本：`v0.0.1-beta.1`
- RC版本：`v0.0.1-rc.1`
- Release版本：`v0.0.1`
