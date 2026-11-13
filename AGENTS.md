# AGENTS.md

项目介绍见 [README.md](./README.md)，仓库快照见 [STATUS.md](./STATUS.md)，维护流程见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 资产管理

- **按指定维护**：根据用户指定准确维护对应仓库、文件夹和文件
- **默认落点**：未指定位置时，写入语境仓库的 default 板块（`data/context/default/`）
- **journal / profile 禁止移动**：事实源住 `data/`（`data/journal/`、`data/profile/` 等），不移入任何 app 仓、不改事实源位置——长期规矩，以本条为准；`data/context/<板块>/journal|profile/` 是草稿箱，定稿后按惯例归位事实源，不属移动
- **仓库分工与归属细则**：见 [CONTRIBUTING.md](./CONTRIBUTING.md) 的「仓库分工与资产归属」

## 记忆流转

长期记忆只有两个流向，命令与记账细则见 [CONTRIBUTING.md](./CONTRIBUTING.md) 的「记忆流转」：

- **归位**：`data/context/` 草稿定稿后按板块平移进目标长期记忆仓库——原样不改写，context 侧只留当日草稿
- **归档**：长期记忆仓库中提炼完成或失活的内容迁入 `data/archive/{分层}/{板块}/`——只迁移、不删除

## 语境仓库（data/context）

语境仓库是**其他仓库的草稿箱**——内容先在这里起草，定稿后归入真正归属的仓库与分层。

- **按板块组织**：目录与业务板块同名（default / qtadmin / qtclass / qtcloud / qtconsult / qtdata），板块内按分层建子目录（insight / intention / journal / brochure 等）
- **不是事实源**：草稿的正式归属在对应仓库（如 `data/insight/`、`data/intention/` 或各领域/业务仓库）；查权威口径去归属仓库，不在这里

## AI 操作经验

- **新工具先跑 init**：使用不熟悉的 CLI 框架或配置文件，先执行 `tool init` 看官方生成的模板，不凭经验臆造格式
- **命令先求证**：CLI 参数使用前先 `tool --help` 或查官方文档确认
- **验证到终点**：CI 通过不等于可访问——部署后确认最终 URL 返回 200，产出物含 `index.html`
