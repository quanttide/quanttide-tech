# 版本发布操作指南

## Skill 位置

发布技能（遵循 [v0.1.1 版标准](https://github.com/quanttide/quanttide-specification-of-business-entity/blob/v0.1.1/devops/release.md)）已提炼到 gallery 仓库：[v0.0.3](https://github.com/quanttide/quanttide-gallery-of-business-entity/blob/v0.0.3/devops/release/SKILL.md)

## 使用方法

1. 复制 skill 到本地 `.agents/skills/release/SKILL.md`
2. 提示 opencode 使用 release 技能执行发布

```bash
cp docs/gallery/devops/release/SKILL.md .agents/skills/release/SKILL.md
```

## 操作方法

使用 opencode 执行发布：

1. 让 opencode 读取最新版本的发布规范文档链接
2. opencode 会根据规范自动执行：更新 CHANGELOG.md、创建 Git 标签、推送标签、创建 GitHub Release
3. 检查 Release 链接是否正确生成