# STATUS

仓库当前快照，供 Agent 与协作者快速了解现状。快照有时效，以最新提交为准；维护流程见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

> 快照日期：2026-09-10

## 仓库形态

主仓库只挂当前活跃开发的产品与知识资产，共 24 个子模块（apps 5、data 11、docs 6、examples 1、packages 1），明细见 [README.md](./README.md)。产品仓库独立开发与发布（各自走 CI 与 qtcloud-devops 发布流程），不依赖主仓库聚合；取消挂载的产品（qtmedia、qtcrowd、qtrecurit）在 GitHub 独立维护，本地目录已清空。

## qtdata 差距分析

基于三份来源的交叉对比：

| 来源 | 角色 | 内容特征 |
|------|------|----------|
| `data/journal/qtdata/` | 业务日记 | 真实项目对话、CEO商业模式思考、战略讨论 |
| `data/intention/qtdata/index.md` | 战略意图 | 体系化愿景——平台化、三方体系、信用定价权 |
| `apps/qtdata/src/cli/` | 当前实现 | 本地CLI骨架，Markdown→结构化数据 |
