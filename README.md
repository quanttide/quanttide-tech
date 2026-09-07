# 量潮科技第二大脑

量潮科技第二大脑是量潮的组织知识系统：开源工作档案（data/）与知识库（docs/）作为单一事实源，产品应用（apps/）承载业务与治理，实验室（examples/）承载探索。

## 子模块

### 产品应用（apps）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| qtadmin | `apps/qtadmin/` | 量潮管理后台——治理思想的平台化载体 |
| qtclass | `apps/qtclass/` | 量潮课堂——学习平台 |
| qtcloud | `apps/qtcloud/` | 量潮云——云服务与 DevOps |
| qtcrowd | `apps/qtcrowd/` | 量潮众包——渠道与代理众包 |
| qtdata | `apps/qtdata/` | 量潮数据——数据服务 |
| qtmedia | `apps/qtmedia/` | 量潮媒体中心 |
| qtrecurit | `apps/qtrecurit/` | 量潮招聘——招聘与评估平台 |
| qtweb | `apps/qtweb/` | 量潮官网 |

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

### 实验室（examples）

| 子模块 | 路径 | 说明 |
|--------|------|------|
| default | `examples/default/` | 公司实验室——实验与探索 |

## 初始化

```bash
git submodule update --init --recursive
```
