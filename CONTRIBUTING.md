# CONTRIBUTING

项目介绍见 [README](./README.md)，AI 工作规则见 [AGENTS](./AGENTS.md)。

## 子模块维护

主仓库指针只记录当前验证过的子模块状态。内容改完后按「先子模块、后主仓库」的顺序提交推送。

- **指针提交**：子模块内提交推送后，回主仓库 `git add <子模块路径>`，以 `chore: update <name> submodule` 提交
- **新增挂载**：更新 `.gitmodules` 与 `README.md` 子模块表，并把新路径加入 `docs/myst.yml` 的 `project.exclude`、在 `docs/index.md` 补链接
- **取消挂载**：`git submodule deinit` + `git rm` + 清理 `.git/modules`，并同步 README

操作命令见 [devops-submodule](./.agents/skills/devops-submodule/SKILL.md)。

## 文档门户

- 部署地址：<https://quanttide.github.io/quanttide-tech/>
- `docs/index.md` 是门户首页，按记忆模型分类列出子模块链接
- 构建与部署流程见 [docs-deploy](./.agents/skills/docs-deploy/SKILL.md)

## 发布规范

CHANGELOG 中涉及子模块更新的条目，必须标注目标版本号：

```markdown
### 变更
- 更新子模块：qtadmin(v0.2.0)、tutorial(v0.0.3)、roadmap(v0.0.2)
```

版本号取自子模块自身的 git tag；未发布的子模块用 commit SHA 前 7 位。发布流程见 [devops-release](./.agents/skills/devops-release/SKILL.md)。

## SKILL 维护

AI Agent 技能存放在 `.agents/skills/`，遵循 [Agent Skills 规范](https://agentskills.io/specification)。

## 提交约定

提交即推送（主仓库与子模块都推），除非明确说明只提交不推。提交信息用 Conventional Commits，规范见 [devops-commit](./.agents/skills/devops-commit/SKILL.md)。
