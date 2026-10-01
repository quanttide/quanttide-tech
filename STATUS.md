# STATUS

仓库当前快照，供 Agent 与协作者快速了解现状。快照有时效，以最新提交为准；维护流程见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

> 快照日期：2026-10-01

## 仓库形态

主仓库只挂当前活跃开发的产品与知识资产，共 25 个子模块（apps 6、data 11、docs 6、examples 1、packages 1），明细见 [README.md](./README.md)。

- 产品仓库独立开发与发布（各自走 CI 与 qtcloud-devops 发布流程），不依赖主仓库聚合
- 取消挂载的产品（qtmedia、qtcrowd、qtrecurit）在 GitHub 独立维护
- 退役的工具集（quanttide-project-toolkit）已取消挂载、本地目录清空
