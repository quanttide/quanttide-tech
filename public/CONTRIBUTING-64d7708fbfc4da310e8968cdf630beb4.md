# 贡献指南

欢迎贡献本项目！

## 贡献方式

- 报告问题：通过 GitHub Issues 反馈
- 提交修改：通过 Pull Request 贡献

## 提交流规范

### 文件命名

- 使用小写字母
- 单词间用下划线 `_` 分隔

### 提交信息规范

- 使用中文或英文，保持一致性

## 提交流程

1. **Fork 仓库**
2. **创建分支**：`git checkout -b feature/xxx`
3. **进行修改**
4. **提交更改**
5. **推送分支**：`git push origin branch-name`
6. **创建 Pull Request**

## 发布流程

1. **检查 CHANGELOG**：查看已有版本记录格式
2. **更新 CHANGELOG**：在 `[Unreleased]` 下新增版本块
3. **提交推送**：确保所有变更已推送到远程
4. **创建 Release**：
   ```bash
   gh release create <version> --title "v<version>" --notes-file CHANGELOG.md --draft
   ```
   正式发布：`gh release edit <tag> --draft=false`

## 版本规范

遵循语义化版本（SemVer）：`主版本.次版本.修订号`

| 类型 | 场景 | 示例 |
|------|------|------|
| 修订号 | 错别字修正 | 0.0.1 → 0.0.2 |
| 次版本 | 新增内容 | 0.0.1 → 0.1.0 |
| 主版本 | 架构调整 | 0.1.0 → 1.0.0 |

## 联系方式

如有疑问，可通过 GitHub Issues 联系维护者。
