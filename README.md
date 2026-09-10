# 量潮科技第二大脑

量潮科技第二大脑是量潮的组织知识系统：开源工作档案（data/）与知识库（docs/）作为单一事实源，产品应用（apps/）承载业务与治理，实验室（examples/）承载探索。

## 产品研发方法论

本仓库使用**数据驱动的产品研发**方法，核心为档案数据闭环：

```
工作档案 → 数据建模 → 半结构化契约 → 各端独立开发 → 新数据回流档案
```

方法定义在 `docs/handbook/qtcloud/product.md`（意图 → 流程 → 验收 三段论）。

- **工作档案是单一事实源**——档案库是业务数据和知识的权威来源
- **半结构化数据作为契约**——JSON/YAML 格式的资产定义作为各端开发的接口契约
- **增量回写**——开发过程中产生的结构化新数据回写档案库，形成数据循环

## 内容库分工

```
data/journal（实录）→ data/insight（洞察提炼）→ docs/essay（成品叙事）
```

单向流动，各层独立成立。essay 不二次沉淀到 insight——文章是洞察的成品形态，写完即终点，不再回灌。

## 特殊文件

| 文件 | 用途 |
|------|------|
| `AGENTS.md` | AI Agent 工作规则 |
| `STATUS.md` | 仓库当前快照 |
| `CONTRIBUTING.md` | 贡献指南、维护流程与 SKILL 维护 |
| `CHANGELOG.md` | 版本变更记录 |
| `index.md` | MyST 站点首页导航门户，按角色（业务/职能）组织链接。修改时同步新增/删除的子模块或文件 |

## 子模块

### 产品应用（apps）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| qtadmin | `apps/qtadmin/` | 量潮管理后台——治理思想的平台化载体 |
| qtclass | `apps/qtclass/` | 量潮课堂——学习平台 |
| qtcloud | `apps/qtcloud/` | 量潮云——云服务与 DevOps |
| qtdata | `apps/qtdata/` | 量潮数据——数据服务 |
| qtweb | `apps/qtweb/` | 量潮官网 |

以下产品仓库已取消子模块挂载，独立维护：

- 量潮媒体中心 qtmedia：`https://github.com/quanttide/qtmedia`
- 量潮众包 qtcrowd：`https://github.com/quanttide/qtcrowd`
- 量潮招聘 qtrecurit：`https://github.com/quanttide/qtrecurit`

### 档案库（data）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| archive | `data/archive/` | 工作归档——历史数据与文档归档 |
| brochure | `data/brochure/` | 企业宣传册——面向客户与潜在客户的业务介绍 |
| context | `data/context/` | 工作语境 |
| history | `data/history/` | 品牌故事 |
| insight | `data/insight/` | 工作洞察——实践提炼的洞察 |
| intention | `data/intention/` | 工作意图——「我们要什么、为什么」 |
| journal | `data/journal/` | 工作日志——业务实录 |
| library | `data/library/` | 图书馆——公开资料参考源 |
| profile | `data/profile/` | 工作简介——业务数据与资产定义档案 |
| report | `data/report/` | 工作报告——运营报告 |
| roadmap | `data/roadmap/` | 工作蓝图——产品路线图 |

### 知识库（docs）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| bylaw | `docs/bylaw/` | 工作章程——治理规范性文件 |
| essay | `docs/essay/` | 工作札记与工作论文——成品叙事 |
| gallery | `docs/gallery/` | 工作案例 |
| handbook | `docs/handbook/` | 工作手册——企业经营各方面文档 |
| specification | `docs/specification/` | 工程标准——流程、文档格式、工具规范 |
| tutorial | `docs/tutorial/` | 工作教程 |

### 工具集（packages）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| quanttide-tech-toolkit | `packages/quanttide-tech-toolkit/` | 量潮技术工具箱——跨业务、跨领域流程整合 |

### 实验室（examples）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| default | `examples/default/` | 公司实验室——实验与探索 |

## 初始化

```bash
git submodule update --init --recursive
```
