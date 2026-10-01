# AGENTS.md

项目介绍见 [README.md](./README.md)，仓库快照见 [STATUS.md](./STATUS.md)，维护流程见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

## 资产管理

根据用户指定准确维护对应仓库、文件夹和文件。
默认使用语境仓库（data/context文件夹）的default文件夹。

## 语境仓库（data/context）

语境仓库是**其他仓库的草稿箱**——内容先在这里起草，定稿后归入真正归属的仓库与分层。

- **按板块组织**：目录与业务板块同名（default / qtadmin / qtclass / qtcloud / qtconsult / qtdata），板块内按分层建子目录（insight / intention / journal / brochure 等）
- **不是事实源**：草稿的正式归属在对应仓库（如 `data/insight/`、`data/intention/` 或各领域/业务仓库）；查权威口径去归属仓库，不在这里
- **默认板块为 default**

## AI 操作经验

- **新工具先跑 init**：使用不熟悉的 CLI 框架或配置文件，先执行 `tool init` 看官方生成的模板，不凭经验臆造格式
- **命令先求证**：CLI 参数使用前先 `tool --help` 或查官方文档确认
- **验证到终点**：CI 通过不等于可访问——部署后确认最终 URL 返回 200，产出物含 `index.html`
