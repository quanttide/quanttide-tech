# CONTRIBUTING

项目介绍见 [README](./README.md)，AI 工作规则见 [AGENTS](./AGENTS.md)。

## 子模块维护

主仓库指针只记录当前验证过的子模块状态。内容改完后按「先子模块、后主仓库」的顺序提交推送。

- **指针提交**：子模块内提交推送后，回主仓库 `git add <子模块路径>`，以 `chore: update <name> submodule` 提交
- **新增挂载**：更新 `.gitmodules` 与 `README.md` 子模块表，并把新路径加入根目录 `myst.yml` 的 `project.exclude`、在 `index.md` 补链接
- **取消挂载**：`git submodule deinit` + `git rm` + 清理 `.git/modules`，并同步 README

操作命令见 [devops-submodule](./.agents/skills/devops-submodule/SKILL.md)。

## 仓库分工与资产归属

- **qtcloud**：职能执行仓——围绕 execute / connect（发布流水线、数据连接、消息推送），价值在触发执行
- **qtadmin**：监控面板——围绕 journal / profile 等范畴与资产做指标与验收展示，只读 `data/` 数据层
- **journal / profile 禁止移动**：住 `data/`（`data/journal/`、`data/profile/`、`data/context/<板块>/journal|profile/`），不移入任何 app 仓

## 记忆流转

长期记忆只有两个流向：**草稿定稿归位**（context → 长期记忆仓库）与**失活归档**（长期记忆仓库 → archive）。两者都只迁移、不删除，也不违反上面的禁移动条款（禁的是搬进 app 仓，归位与归档是正常流动）。

### context → 长期记忆仓库

context 是各长期记忆仓库的草稿箱，轴向与归位方向相反（`context/{板块}/{分层}/` → `data/{分层}/{板块}/`），细则见 [data/context/README](./data/context/README.md)。

1. **拉新**：`git submodule update --init --remote -- data/context`
2. **归位**：定稿日志按板块平移进目标仓，原样不改写；context 侧只保留当日草稿
   - 分流：管理后台（qtadmin）不单独立目录，日志按分流入 `journal/default/`；已归档业务线直移 `data/archive/{分层}/{板块}/`
3. **提交推送**：目标仓与 context 仓先后各自提交推送（context 处于分离头指针时用 `git push origin HEAD:main`），回主仓库 `git add data/context data/<目标仓>` 更新指针
4. **记账**：目标仓 CHANGELOG 记一行归位记录（篇数、日期范围、分流去向）

### 长期记忆仓库 → archive

提炼完成或失去活性的内容迁入 `data/archive/{分层}/{板块}/`，内容不删除、只迁移。

- **触发**：以各仓归档约定为准——日志完成提炼（journal）、意图失去活性（intention）、板块整体失活（profile 等）
- **提交推送**：源仓删除与 archive 仓新增各自提交推送，回主仓库 `git add data/<源仓> data/archive` 更新指针
- **记账**：archive 仓 CHANGELOG 记归档来源

## 文档门户

- 部署地址：<https://quanttide.github.io/quanttide-tech/>
- `index.md` 是门户首页，按记忆模型分类列出子模块链接
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
